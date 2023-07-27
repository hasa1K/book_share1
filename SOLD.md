单一原则：
一个类或模块应该只有一个改变的理由，这意味着它应该只有一个责任。通过遵循这一原则，代码变得更加模块化、更易于理解，并且在更改时不易出现错误。
开放封闭原则：
软件实体应该对扩展开放，但对修改关闭。这意味着模块的行为在不修改其他源码的情况下扩展。通常使用抽象和组合实现。
里氏替换原则：
派生的结构或类或子类型必须可替换其基结构或类或超类型，而不影响程序的正确性。
接口隔离原则：
结构体不应实现它不需要的接口和方法。可以减少模块之间的相互依赖，便于理解和维护代码。
依赖倒置原则:
高层的应用应该依赖于接口，而不是具体的函数。有利于程序的解耦和可维护性。

##### 单一职责原则
```go
type PaymentService struct {}

func (ps PaymentService) ProcessPayment(amount float64) {

}

type InvoiceService struct{}
func (is InvoiceService) CreateInvoice(amount float64) {

}
```

##### 开放封闭原则
```go
type PaymentMethod interface {
	Pay(amount float64)
}

type CreditCard struct{}

func (cc CreditCard) Pay(amount float64) {

}

type PayPal struct {}

func (pp PayPal) Pay(amount float64) {

}

func ProcessPayment(method PaymentMethod, amount float64) {
	method.Pay(amount)
}
```

##### 里氏替换原则

下面的代码可以编译不会通过，因为 InvalidPaymentMethod 没有实现 PaymentMethod 接口。
```go
package main

// Bad examples

type PaymentMethod interface {
   Pay(amount float64)
}

type CreditCard struct{}

func (cc CreditCard) Pay(amount float64) {
   // Process credit card payment
}

type InvalidPaymentMethod struct{}

func (ipm InvalidPaymentMethod) InvalidPay(amount float64) {
   // Invalid payment method implementation
}

func ProcessPayment(method PaymentMethod, amount float64) {
   method.Pay(amount)
}

func main() {
   cc := CreditCard{}
   ProcessPayment(cc, 100)

   ipm := InvalidPaymentMethod{}
   ProcessPayment(ipm, 100)
}
```

##### 接口分离原则
```go
type OnlinePaymentMethod interface {
	PayOnline(amount float64)
}

type OfflinePaymentMethod interface {
	PayOffline(amount float64)
}

type PayPal struct {}

func (pp PayPal) PayOnline(amount float64) {

}

type Cash struct {}

func(c Cash) PayOffline(amout float64) {

}
```

##### 依赖倒置原则
```go
package main

// Good examples

type PaymentMethod interface {
   Pay(amount float64)
}

type CreditCard struct{}

func (cc CreditCard) Pay(amount float64) {
   // Process credit card payment
}

type PayPal struct{}

func (pp PayPal) Pay(amount float64) {
   // Process PayPal payment
}

type PaymentService struct {
   method PaymentMethod
}

func (ps *PaymentService) SetPaymentMethod(method PaymentMethod) {
   ps.method = method
}

func (ps PaymentService) ProcessPayment(amount float64) {
   ps.method.Pay(amount)
}

func main() {
   cc := CreditCard{}
   pp := PayPal{}

   paymentService := PaymentService{}
   
   paymentService.SetPaymentMethod(cc)
   paymentService.ProcessPayment(100)
   
   paymentService.SetPaymentMethod(pp)
   paymentService.ProcessPayment(200)
}
```
