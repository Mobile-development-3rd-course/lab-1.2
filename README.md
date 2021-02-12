<div align = "center"><strong>
Міністерство освіти і науки України<br>
Національний технічний університет України<br>
«Київський політехнічний інститут ім. Ігоря Сікорського»<br>
Факультет інформатики та обчислювальної техніки<br>
Кафедра обчислювальної техніки<br><br><br><br>
</strong></div>

<div align = "center" bold = ""><strong>ЛАБОРАТОРНА РОБОТА № 1.2</strong><br><br>
з дисципліни «Розроблення клієнтських додатків для мобільних платформ»<br>
на тему «Основи Swift»</div><br><br><br><br>

<div align = "right" >Виконав:<br>
студент ІІІ курсу ФІОТ<br>                        
групи ІП-84<br>                                
Андрейченко Кирило<br>
номер залікової книжки: 8401<br></div><br><br><br><br>

<div align = "center">Київ – 2021</div><br><br><br><br>

<strong>Варіант роботи номер 2.</strong><br>
<strong>Скріншоти роботи застосунка:</strong><br>
1. Тести частина 1<br>
<p align = "center"><img src="https://i.imgur.com/QWeb94R.png" alt="first part"/></p><br>

2. Тести частина 2<br>
<p align = "center"><img src="https://i.imgur.com/yqw3fuh.png" alt="seconds part"/></p><br>

<strong>Лістинг коду:</strong><br>

<i>ProgrammingAssignment1_2.playground</i>
```swift

import Foundation

// Частина 1
let studentsStr = "Дмитренко Олександр - ІП-84; Матвійчук Андрій - ІВ-83; Лесик Сергій - ІО-82; Ткаченко Ярослав - ІВ-83; Аверкова Анастасія - ІО-83; Соловйов Даніїл - ІО-83; Рахуба Вероніка - ІО-81; Кочерук Давид - ІВ-83; Лихацька Юлія- ІВ-82; Головенець Руслан - ІВ-83; Ющенко Андрій - ІО-82; Мінченко Володимир - ІП-83; Мартинюк Назар - ІО-82; Базова Лідія - ІВ-81; Снігурець Олег - ІВ-81; Роман Олександр - ІО-82; Дудка Максим - ІО-81; Кулініч Віталій - ІВ-81; Жуков Михайло - ІП-83; Грабко Михайло - ІВ-81; Іванов Володимир - ІО-81; Востриков Нікіта - ІО-82; Бондаренко Максим - ІВ-83; Скрипченко Володимир - ІВ-82; Кобук Назар - ІО-81; Дровнін Павло - ІВ-83; Тарасенко Юлія - ІО-82; Дрозд Світлана - ІВ-81; Фещенко Кирил - ІО-82; Крамар Віктор - ІО-83; Іванов Дмитро - ІВ-82"

// Завдання 1
// Заповніть словник, де:
// - ключ – назва групи
// - значення – відсортований масив студентів, які відносяться до відповідної групи

var studentsGroups: [String: [String]] = [:]
// Ваш код починається тут

studentsStr.split(separator: ";").forEach({item in
    let studentAndGroup: [String] = item.components(separatedBy: "- ")
    
    if var student = studentAndGroup.first, var group = studentAndGroup.last {
        student = student.trimmingCharacters(in: .whitespacesAndNewlines)
        group = group.trimmingCharacters(in: .whitespacesAndNewlines)
        studentsGroups[group, default: [String]()].append(student)
    } else {
        return
    }
})

studentsGroups.map ({ (key, value) in
    return studentsGroups[key] = value.sorted()
})

// Ваш код закінчується тут
print("--------------------------------------------------------------------- Частина 1 ---------------------------------------------------------------------")
print()
print("Завдання 1")
print(studentsGroups)
print()

// Дано масив з максимально можливими оцінками

let points: [Int] = [12, 12, 12, 12, 12, 12, 12, 16]

// Завдання 2
// Заповніть словник, де:
// - ключ – назва групи
// - значення – словник, де:
//   - ключ – студент, який відносяться до відповідної групи
//   - значення – масив з оцінками студента (заповніть масив випадковими значеннями, використовуючи функцію `randomValue(maxValue: Int) -> Int`)

func randomValue(maxValue: Int) -> Int {
    switch(arc4random_uniform(6)) {
    case 1:
        return Int(ceil(Float(maxValue) * 0.7))
    case 2:
        return Int(ceil(Float(maxValue) * 0.9))
    case 3, 4, 5:
        return maxValue
    default:
        return 0
    }
}

var studentPoints: [String: [String: [Int]]] = [:]
// Ваш код починається тут

for (key, value) in studentsGroups {
    value.forEach({ item in
        let pointsOfStudent = points.map({ randomValue(maxValue: $0) })
        studentPoints[key, default: [String: [Int]]()].updateValue(pointsOfStudent, forKey: item)
    })
}

// Ваш код закінчується тут

print("Завдання 2")
print(studentPoints)
print()

// Завдання 3
// Заповніть словник, де:
// - ключ – назва групи
// - значення – словник, де:
//   - ключ – студент, який відносяться до відповідної групи
//   - значення – сума оцінок студента

var sumPoints: [String: [String: Int]] = [:]

// Ваш код починається тут

studentPoints.map({ group, studentPoints in
    var sumPointsOfStudent: [String: Int] = [:]
    
    studentPoints.forEach({ (student, points) in
        let sum = points.reduce(0, +)
        sumPointsOfStudent.updateValue(sum, forKey: student)
    })
    
    sumPoints.updateValue(sumPointsOfStudent, forKey: group)
})

// Ваш код закінчується тут

print("Завдання 3")
print(sumPoints)
print()

// Завдання 4
// Заповніть словник, де:
// - ключ – назва групи
// - значення – середня оцінка всіх студентів групи

var groupAvg: [String: Float] = [:]

// Ваш код починається тут

for (key, value) in sumPoints {
    groupAvg.updateValue(Float(value.values.reduce(0, +)) / Float(value.count), forKey: key)
}

// Ваш код закінчується тут

print("Завдання 4")
print(groupAvg)
print()

// Завдання 5
// Заповніть словник, де:
// - ключ – назва групи
// - значення – масив студентів, які мають >= 60 балів

var passedPerGroup: [String: [String]] = [:]

// Ваш код починається тут

sumPoints.forEach( {group, studentPointsSum in
    let filteredStudents = studentPointsSum.filter({_, sum in
        return sum >= 60
    }).map{ $0.key }
    
    passedPerGroup[group] = filteredStudents
})

// Ваш код закінчується тут
print("Завдання 5")
print(passedPerGroup)
print()

// Частина 2
enum Direction {
    case latitude
    case longitude
}

class CoordinateKA {
    
    var direction: Direction
    var degrees: Int
    var minutes, seconds: UInt
    
    var directionCharacter: String {
        switch direction {
        case .latitude:
            return degrees >= 0 ? "E" : "W"
        case .longitude:
            return degrees >= 0 ? "N" : "S"
        }
    }
    
    init() {
        degrees = 0
        minutes = 0
        seconds = 0
        
        direction = .latitude
    }
    
    init?(direction: Direction, degrees: Int, minutes: UInt, seconds: UInt) {
        let maxDegree: Int
        switch direction {
        case .longitude:
            maxDegree = 180
        case .latitude:
            maxDegree = 90
        }
        guard (minutes <= 59) && (seconds <= 59) && (abs(degrees) <= maxDegree) else {
            return nil
        }
        
        self.minutes = minutes
        self.seconds = seconds
        self.direction = direction
        self.degrees = degrees
    }
    
    private func makeDecimalDegree() -> Float {
        var decimalDegree: Float
        if (degrees >= 0) {
            decimalDegree = (Float(seconds) / 3600) + (Float(minutes) / 60) + Float(degrees)
        } else {
            decimalDegree = -(Float(seconds) / 3600) - (Float(minutes) / 60) + Float(degrees)
        }
        
        return decimalDegree
    }
    
    private func makeDegreesMinutesSeconds(mid: Float, direction: Direction) -> CoordinateKA {
        let degrees = Int(floor(mid))
        let minutes = UInt(60 * Float(mid - Float(degrees)))
        let seconds = UInt(3600 * Float(mid - Float(degrees)) - 60 * Float(minutes))
        
        return CoordinateKA(direction: direction, degrees: degrees, minutes: minutes, seconds: seconds)!
    }
    
    func a() -> String {
        return "\(abs(degrees))°\(minutes)′\(seconds)″ \(directionCharacter)"
    }
    
    func b() -> String {
        return "\(abs(makeDecimalDegree()))° \(directionCharacter)"
    }
    
    func c(secondCoordinate: CoordinateKA) -> CoordinateKA? {
        guard direction == secondCoordinate.direction else {
            return nil
        }
        
        let mid: Float = (makeDecimalDegree() + secondCoordinate.makeDecimalDegree()) / 2
        return makeDegreesMinutesSeconds(mid: mid, direction: direction)
    }
    
    static func d(firstCoordinate: CoordinateKA, secondCoordinate: CoordinateKA) -> CoordinateKA? {
        return firstCoordinate.c(secondCoordinate: secondCoordinate)
    }
    
}


print("--------------------------------------------------------------------- Частина 2 ---------------------------------------------------------------------")

// TESTS

// test 1
print("test 1")
// 18
let coordinate1 = CoordinateKA(direction: .latitude, degrees: 80, minutes: 30, seconds: 29)
let coordinate2 = CoordinateKA()

// 16 (a)
print("16 (a) – coordinate 1: ", coordinate1!.a())
print("16 (a) – coordinate 2: ", coordinate2.a())

// 16 (b)
print("16 (b) – coordinate 1: ", coordinate1!.b())
print("16 (b) – coordinate 2: ", coordinate2.b())

// 16 (c)
print("16 (c): ", coordinate1!.c(secondCoordinate: coordinate2)!.a())

// 17 (a)
print("17 (a):", CoordinateKA.d(firstCoordinate: coordinate1!, secondCoordinate: coordinate2)!.a() )
print()
print("test 2")
// test 2

// 18
let coordinate3 = CoordinateKA(direction: .longitude, degrees: 40, minutes: 40, seconds: 40)
let coordinate4 = CoordinateKA(direction: .longitude, degrees: 50, minutes: 20, seconds: 21)

// 16 (a)
print("16 (a) – coordinate 1: ", coordinate3!.a())
print("16 (a) – coordinate 2: ", coordinate4!.a())

// 16 (b)
print("16 (b) – coordinate 1: ", coordinate3!.b())
print("16 (b) – coordinate 2: ", coordinate4!.b())

// 16 (c)
print("16 (c): ", coordinate3!.c(secondCoordinate: coordinate4!)!.a())

// 17 (a)
print("17 (a):", CoordinateKA.d(firstCoordinate: coordinate3!, secondCoordinate: coordinate4!)!.a() )

```
<strong>Висновок:</strong><br>
На лабораторній роботі номер 1.2 я познайомився з основами мови програмування Swift, виконав різноманітні задачі.
