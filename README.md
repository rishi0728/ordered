import Foundation



struct Time: Comparable, Hashable {
    var hour: Int
    var minute: Int
    
    static func < (firt: Time, second: Time) -> Bool {
        if firt.hour == second.hour {
            return firt.minute < second.minute
        }
        return firt.hour < second.hour
    }
    
    static func <= (first: Time, second: Time) -> Bool {
        return first < second || first == second
    }
    
    static func == (first: Time, second: Time) -> Bool {
        return first.hour == second.hour && first.minute == second.minute
    }
    
    func hash(into hasher: inout Hasher) {
        hasher.combine(hour)
        hasher.combine(minute)
    }
}

struct Order {
    var orderId: String
    var entryTime: Time
    
}

class Collection {
    private var orderDictionary: [Time: [Order]] = [:]
    
    func addOrder(order: Order) {
        orderDictionary[order.entryTime, default: []].append(order)
    }
    
    func search(startTime: Time, endTime: Time) -> [Order] {
        var result: [Order] = []
        
        for (time, orders) in orderDictionary {
            if startTime <= time && time <= endTime {
                result.append(contentsOf: orders)
            }
        }
        
        return result
    }
}
let collection = Collection()

let order1 = Order(orderId: "O1", entryTime: Time(hour: 10, minute: 15))


let order2 = Order(orderId: "O2", entryTime: Time(hour: 10, minute: 15))


let order3 = Order(orderId: "O3", entryTime: Time(hour: 10, minute: 15))

let order4 = Order(orderId: "O4", entryTime: Time(hour: 9, minute: 15))


let order5 = Order(orderId: "O7", entryTime: Time(hour: 12, minute: 30))


let order6 = Order(orderId: "O12", entryTime: Time(hour: 7, minute: 30))


let order7 = Order(orderId: "O314", entryTime: Time(hour: 7, minute: 24))


collection.addOrder(order: order1)


collection.addOrder(order: order2)


collection.addOrder(order: order3)


collection.addOrder(order: order4)


collection.addOrder(order: order5)


collection.addOrder(order: order6)


collection.addOrder(order: order7)

let startTime = Time(hour: 9, minute: 20)


let endTime = Time(hour: 10, minute: 16)

let ordersFromCollection = collection.search(startTime: startTime, endTime: endTime)

for order in ordersFromCollection {


    print("Order ID: \(order.orderId), Entry Time: \(order.entryTime.hour):\(order.entryTime.minute)")


}
