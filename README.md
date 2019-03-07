# appvvf
cc
import MapKit

class CustomAnnotation: NSObject, MKAnnotation {
    
    var coordinate: CLLocationCoordinate2D
    
    var title: String? {
        return locationLabel
    }      // Basically, this takes your locationLabel, and displays "returns" it as the CustomAnnotation Title - MKAnnotation has an optional title function already built-in.
    
    var locationDescription: String?
    var locationLabel: String?
    
    init(locationLabel: String, coordinate: CLLocationCoordinate2D, locationDescription: String) {
        self.locationLabel = locationLabel
        self.coordinate = coordinate
        self.locationDescription = locationDescription
  }
  
}

VIEW CONTROLLER

import UIKit
import MapKit

class ViewController: UIViewController {
  
  @IBOutlet weak var mapView: MKMapView!
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    mapView.delegate = self
    
    //Get coordinates
    let bournemouthCoord = CLLocationCoordinate2D(latitude: 50.716440, longitude: -1.875655)
    let londonCoord = CLLocationCoordinate2D(latitude: 51.507517, longitude: -0.118965)
    let manchesterCoord = CLLocationCoordinate2D(latitude: 53.483959, longitude: -2.244644)
    let glasgowCoord = CLLocationCoordinate2D(latitude: 55.859238, longitude: -4.296141)
    //Create some annotations from the coordinates
    let parisCoord = CLLocationCoordinate2D(latitude: 48.8566101, longitude: 2.3514992)
    let sicilyCoord = CLLocationCoordinate2D(latitude: 37.587794, longitude: 14.155048)
    let kandaharCoord = CLLocationCoordinate2D(latitude: 31.6257718, longitude: 65.7144771)
    let gizaCoord = CLLocationCoordinate2D(latitude: 30.0170059, longitude: 31.2134513)
    let newyorkCoord = CLLocationCoordinate2D(latitude: 40.7308619, longitude: -73.9871558)
    let lasvegasCoord = CLLocationCoordinate2D(latitude: 36.1672446, longitude: -115.1490207)
    let alaskaCoord = CLLocationCoordinate2D(latitude: 64.4459613, longitude: -149.680909)
    let seattleCoord = CLLocationCoordinate2D(latitude: 47.6038321, longitude: -122.3300624)
    let hollywoodCoord = CLLocationCoordinate2D(latitude: 34.093214, longitude: -118.3196124)
    
    
    let bournemouthAnnotation = CustomAnnotation(locationLabel: "Bournemouth", coordinate: bournemouthCoord, locationDescription: "Hello")
    let londonAnnotation = CustomAnnotation(locationLabel: "London", coordinate: londonCoord, locationDescription: "Alright,mate?")
    let manchesterAnnotation = CustomAnnotation(locationLabel: "Manchester", coordinate: manchesterCoord, locationDescription: "3")
    //Add annotations to the maps as an array
    let glasgowAnnotation = CustomAnnotation(locationLabel: "Glasgow", coordinate: glasgowCoord,  locationDescription: "4")
    let parisAnnotation = CustomAnnotation(locationLabel: "Paris", coordinate: parisCoord, locationDescription: "Bonjour")
    let sicilyAnnotation = CustomAnnotation(locationLabel: "Sicily", coordinate: sicilyCoord, locationDescription: "Ciao")
    let kandaharAnnotation = CustomAnnotation(locationLabel: "Kandahar", coordinate: kandaharCoord, locationDescription: "Hello")
    let gizaAnnotation = CustomAnnotation(locationLabel: "Giza", coordinate: gizaCoord, locationDescription: "Hello")
    let newyorkAnnotation = CustomAnnotation(locationLabel: "New York", coordinate: newyorkCoord, locationDescription: "Hello")
    let lasvegasAnnotation = CustomAnnotation(locationLabel: "Las Vegas", coordinate: lasvegasCoord, locationDescription: "Hello")
    let alaskaAnnotation = CustomAnnotation(locationLabel: "Alaska", coordinate: alaskaCoord, locationDescription: "Hello")
    let seattleAnnotation = CustomAnnotation(locationLabel: "Seattle", coordinate: seattleCoord, locationDescription: "Hello")
    let hollywoodAnnotation = CustomAnnotation(locationLabel: "Hollywood", coordinate: hollywoodCoord, locationDescription: "Hello")
    mapView.addAnnotations([manchesterAnnotation, bournemouthAnnotation, londonAnnotation, glasgowAnnotation, parisAnnotation, sicilyAnnotation, kandaharAnnotation, gizaAnnotation, newyorkAnnotation, lasvegasAnnotation, alaskaAnnotation, seattleAnnotation, hollywoodAnnotation ])
    
   
  }
    
  
  override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
    let vc = segue.destination as! SecondViewController
    vc.annotation = sender as? CustomAnnotation
  }

}

extension ViewController: MKMapViewDelegate {
  
  func mapView(_ mapView: MKMapView, didSelect view: MKAnnotationView) {
    guard let annotation = view.annotation as? CustomAnnotation else { return }
    performSegue(withIdentifier: "Next", sender: annotation)
    mapView.deselectAnnotation(annotation, animated: true)
  }
  
  SECOND VIEW CONTROLLER
  
  import UIKit

class SecondViewController: UIViewController {
    
    @IBOutlet weak var imageView: UIImageView!
    @IBOutlet weak var label: UILabel!
    @IBOutlet weak var locationDescription: UILabel!
    
  var annotation: CustomAnnotation!
  
  override func viewDidLoad() {
    super.viewDidLoad()
    label.text = annotation.locationLabel!
    imageView.image = UIImage(named: annotation.locationLabel!)
    imageView.clipsToBounds = true
    locationDescription.text = annotation.locationDescription
  }
  
}



