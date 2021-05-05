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

Then, Create a CodableStore class 
```Swift
class CodeableStore<M: Codable> {
    var store: M
    
    var key: String
    
    init(key: String, store: M) {
        self.key = key
        self.store = store
    }
    
    func write() {
        do {
            let codable = try JSONEncoder().encode(store)
            UserDefaults.standard.setValue(codable, forKey: key)
        }catch{}
    }
    
    func read() {
        if let value = UserDefaults.standard.value(forKey: key) {
            do {
                store = try JSONDecoder().decode(M.self, from: value as! Data)
            }catch{
                
            }
        }
    }
}
```
Then , lets test it 

```Swift
let myCodableStore = CodeableStore<StoreModel>(key: "myappcodable", store: StoreModel())

myCodableStore.store.apnsToken = "Jowel"

myCodableStore.write()
let myCodableStore1 = CodeableStore<StoreModel>(key: "myappcodable", store: StoreModel())
myCodableStore1.read()
myCodableStore1.store.apnsToken
```
#In iOS App, you can call read at application launch time to get last saved value. 



