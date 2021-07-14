# Learning Solidity by myself

![solid logo](https://media-exp3.licdn.com/dms/image/C4D12AQHrjWDa4m4ILw/article-cover_image-shrink_720_1280/0/1523961294826?e=1631145600&v=beta&t=crxhQm5R8GpQAbclLKqD-PdYPShk2XYDDWfLEu6e9fk)
---
<!-- 
## Content
* แหล่งเรียนรู้
--- -->
แหล่งเรียนรู้
* [Cryptozombies](https://cryptozombies.io/)
* [Document Solidity](https://docs.soliditylang.org/en/v0.8.6/)
* [Medium คุณ Jedsada Tiwongvorakul](https://medium.com/20scoops-cnx/%E0%B8%A1%E0%B8%B2%E0%B8%A3%E0%B8%B9%E0%B9%89%E0%B8%88%E0%B8%B1%E0%B8%81%E0%B8%81%E0%B8%B1%E0%B8%9A-solidity-%E0%B8%82%E0%B8%B1%E0%B9%89%E0%B8%99%E0%B8%9E%E0%B8%B7%E0%B9%89%E0%B8%99%E0%B8%90%E0%B8%B2%E0%B8%99%E0%B8%81%E0%B8%B1%E0%B8%99-6f713b3fb64)
---
### Basic Contract

```
pragma solidity ^0.4.19; 
contract HelloWorld {

}
```
> pragma solidity เอาไว้บอก version ของ compiler

### State Variable & Integers
- uint (Unsigned Integers) ค่า integer ที่ไม่มีเครื่องหมายนั่นคือค่าไม่ติดลบ uint คือ uint256 ซึ่งเราสามารถประกาศเป็น bit ที่น้อยกว่า เช่น uint8, uint16, uint32 แต่ประกาศเพียงแค่ uint ก็เพียงพอ(ในบางกรณี)


### Math Operation
- Add (+) บวก
- Subtraction (-) ลบ
- Multiplication (*) คูณ
- Division (/) หาร
- Modulus / remainder (%) หารเอาเศษ เช่น 13%5 จะได้ 3
- exponential (**) ยกกำลัง

### Struct
เป็นข้อมูลที่มีความซับซ้อนมากขึ้น ใครเคยเขียนภาษา C จะเหมือนกัน

```c
struct Person {
    uint age;
    string name;
}
```
>ตัวอย่างการสร้าง Struct ของคน

### Arrays
มีอยู่ 2 ประเภทคือ 
- Fixed 
- Dynamic

Fixed คือประกาศให้มีความยาวที่จำกัด เช่น
```c
uint[2] fix;
```

Dynamic คือ Arrays ไม่จำกัดขนาด
```c
uint[] dynamic;
```

<เสริม> Public Arrays
การประกาศ arrays ที่มี keyword `public` solidity จะสร้าง getter method อัตโนมัติ

```c
Person[] public people
```
ซึ่ง keyword `public` จะทำให้ array นี้สามารถอ่านได้จาก contract อื่น แต่ไม่สามารถเขียนได้

### Function Declaration
 การประกาศฟังก์ชัน ตัวอย่างเช่น
```js
function eatSomething(string memory _name, uint _amount) public {

}
```
> function ชื่อ eatSomething รับ parameters 2 ตัวคือ string และ uint

>การตั้งชื่อตัวแปรใน params จะตั้งชื่อให้มี underscore( _ )เพื่อที่จะไม่สับสนกับ Global Variable 

`public` keyword | ประกาศว่า function นี้ถูกเรียกใช้งานได้ทุกที่และทุกคน

`memory` keyword | ต้องประกาศเมื่อเรียกใช้ ตัวแปรที่เป็น Reference Type เช่น Arrays, struct, mapping และ String


### Arrays & Struct
สร้าง Arrays ของ Struct ได้แบบนี้
```
struct Person {
  uint age;
  string name;
}

Person[] public people;
```
เราสามารถสร้าง Instance ของ Struct ได้แบบนี้
```
Person aom = Person(20, "aomm");
```
> ซึ่ง Args ของ Person จะเรียงตาม Struct นั้นคือ 20 = age, aomm = name

เราสามารถเพิ่ม `aom` เข้าไปใน Arrays `people` ได้โดย
```js
people.push(aom) 
``` 
><เสริม> Arrays.push() จะ Return ค่า length ของ arrays ออกมา

### Private / Public Functions
ใน Solidity ฟังก์ชั่นจะมีค่า visible เริ่มต้น เป็น `public` ซึ่งทุกคนและทุก contract สามารถเข้าถึงและเรียกใช้งานได้

`private` keyword จะทำให้ function ถูกเรียกใช้งานได้แค่ภายใน contract นี้เท่านั้น
```
uint[] numbers;
function _addNumber(uint _num) private {
    numbers.push(_num);
}
```
>การประกาศ function ที่เป็น private มักจะใช้ชื่อที่นำหน้าด้วย underscore ( _ )
