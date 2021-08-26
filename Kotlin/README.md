# Kotlin

```kt
fun main() {
    
    val age = 5 * 365
    val name = "Rover"
    
    println("Happy Birthday, ${name}!")
    
    // Let's print a cake!
    println("   ,,,,,   ")
    println("   |||||   ")
    println(" =========")
    println("@@@@@@@@@@@")
    println("{~@~@~@~@~}")
    println("@@@@@@@@@@@")
    
    // This prints an empty line.
    println("")

    println("You are already ${age} days old, ${name}!")
    println("${age} days old is the very best age to celebrate!")
}
```

```kt
fun main() {
    printBorder()
    println("Happy Birthday, Jhansi!")
    printBorder2()
}

fun printBorder() {
    println("=======================")
}

fun printBorder2() {
    repeat(23) {
        print("=")
    }
    println()
}

fun printBorder3(border: String) {
    repeat(23) {
        print(border)
    }
    println()
}

fun printBorder4(border: String, timesToRepeat: Int) {
    repeat(timesToRepeat) {
        print(border)
    }
    println()
}
```

https://developer.android.com/courses/pathways/android-basics-kotlin-one#codelab-https://developer.android.com/codelabs/basic-android-kotlin-training-kotlin-birthday-message