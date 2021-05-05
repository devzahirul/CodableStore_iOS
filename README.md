# CodableStore_iOS
Local store using codable protocol 

First create a codable model 
```Swift
struct StoreModel: Codable {
    var apnsToken: String = ""
    var email: String = ""
    var userId: String = ""
}
```
