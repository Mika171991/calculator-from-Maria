# calculator-from-Maria
package main

import (
    "bufio"
    "fmt"
    "os"
    "strconv"
    "strings"
)

var romanToArabic = map[string]int{
    "I": 1, "II": 2, "III": 3, "IV": 4, "V": 5,
    "VI": 6, "VII": 7, "VIII": 8, "IX": 9, "X": 10,
}

var arabicToRoman = map[int]string{
    1: "I", 2: "II", 3: "III", 4: "IV", 5: "V",
    6: "VI", 7: "VII", 8: "VIII", 9: "IX", 10: "X",
}

func main() {
    reader := bufio.NewReader(os.Stdin)
    for {
        fmt.Print("Введите выражение: ")
        expression, _ := reader.ReadString('\n')
        expression = strings.TrimSpace(expression)
        if expression == "exit"  expression == "quit" {
            break
        }
        result, err := calculate(expression)
        if err != nil {
            fmt.Println("Error:", err)
        } else {
            fmt.Println(result)
        }
    }
}

func calculate(expression string) (string, error) {
    parts := strings.Split(expression, " ")
    if len(parts) != 3 {
        return "", fmt.Errorf("invalid expression")
    }

    a, operator, b := parts[0], parts[1], parts[2]

    if isRoman(a) && isRoman(b) {
        return calculateRoman(a, operator, b)
    } else if isArabic(a) && isArabic(b) {
        return calculateArabic(a, operator, b)
    } else {
        return "", fmt.Errorf("mixed numeral systems")
    }
}

func isRoman(s string) bool {
    _, exists := romanToArabic[s]
    return exists
}

func isArabic(s string) bool {
    _, err := strconv.Atoi(s)
    return err == nil
}

func calculateArabic(aStr, operator, bStr string) (string, error) {
    a, _ := strconv.Atoi(aStr)
    b, _ := strconv.Atoi(bStr)
    if a < 1  a > 10  b < 1  b > 10 {
        return "", fmt.Errorf("numbers must be between 1 and 10")
    }
    result, err := performOperation(a, operator, b)
    if err != nil {
        return "", err
    }
    return strconv.Itoa(result), nil
}

func calculateRoman(aStr, operator, bStr string) (string, error) {
    a := romanToArabic[aStr]
    b := romanToArabic[bStr]
    if a < 1  a > 10  b < 1 || b > 10 {
        return "", fmt.Errorf("numbers must be between I and X")
    }
    result, err := performOperation(a, operator, b)
    if err != nil {
        return "", err
    }
    if result < 1 {
        return "", fmt.Errorf("result is less than I")
    }
    return arabicToRoman[result], nil
}

func performOperation(a int, operator string, b int) (int, error) {
    switch operator {
    case "+":
        return a + b, nil
    case "-":
        return a - b, nil
    case "*":
        return a * b, nil
    case "/":
        return a / b, nil
    default:
        return 0, fmt.Errorf("invalid operator")
    }
}
Код, созданный ИИ. Внимательно просмотрите и используйте. Дополнительные сведения о часто задаваемых вопросах.
Этот код создает консольное приложение на языке Go, которое выполняет арифметические операции с арабскими и римскими числами. Программа принимает выражения в формате a + b, a - b, a * b, a / b и выводит результат в соответствующем формате. Если ввод некорректен, программа выдает ошибку и завершает работу.

Попробуйте запустить этот код и посмотрите, как он работает! Если у вас возникнут вопросы или потребуется помощь, дайте знать.
