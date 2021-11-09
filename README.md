# Learning Solidity by myself

![solid logo](https://docs.soliditylang.org/en/v0.8.10/_static/logo.svg)
---
<!-- 
## Content
* แหล่งเรียนรู้
--- -->
แหล่งเรียนรู้
* [Cryptozombies](https://cryptozombies.io/)
* [Document Solidity](https://docs.soliditylang.org/en/v0.8.6/)
* [BlockChian คืออะไร](https://nuuneoi.com/blog/blog.php?read_id=900)
* [Medium คุณ Jedsada Tiwongvorakul](https://medium.com/20scoops-cnx/%E0%B8%A1%E0%B8%B2%E0%B8%A3%E0%B8%B9%E0%B9%89%E0%B8%88%E0%B8%B1%E0%B8%81%E0%B8%81%E0%B8%B1%E0%B8%9A-solidity-%E0%B8%82%E0%B8%B1%E0%B9%89%E0%B8%99%E0%B8%9E%E0%B8%B7%E0%B9%89%E0%B8%99%E0%B8%90%E0%B8%B2%E0%B8%99%E0%B8%81%E0%B8%B1%E0%B8%99-6f713b3fb64)
---
### Basic Contract

```js
pragma solidity ^0.4.19; 
contract HelloWorld {

}
```

> pragma solidity เอาไว้บอก version ของ compiler

### State Variable & Integers

ตัวแปร `state` จะถูกจัดเก็บใน contract storage นั้นหมายถึง มันจะถูกเขียนลงไปใน Eth Blockchain
เหมือนกับการเขียนลง Database

ตัวอย่างเช่น

```js
contract Example {
  // ตัวแปรนี้จะถูกเก็บอย่างถาวรใน Blockchain
  uint myUnsignedInteger = 100; //<- ตัวแปร state
}
```

> ในตัวอย่างนี้เราสร้างตัวแปรชนิด `uint` ที่ชื่อ myUnsignedInteger และกำหนดค่าให้เป็น 100

* uint (Unsigned Integers) ค่า integer ที่ไม่มีเครื่องหมายนั่นคือค่าไม่ติดลบ uint คือ uint256 ซึ่งเราสามารถประกาศเป็น bit ที่น้อยกว่า เช่น uint8, uint16, uint32 แต่ประกาศเพียงแค่ uint ก็เพียงพอ(ในบางกรณี)

### Math Operation

* Add (+) บวก
* Subtraction (-) ลบ
* Multiplication (*) คูณ
* Division (/) หาร
* Modulus / remainder (%) หารเอาเศษ เช่น 13%5 จะได้ 3
* exponential (**) ยกกำลัง

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

* Fixed
* Dynamic

Fixed คือประกาศ Arrays ให้มีความยาวที่จำกัด เช่น

```c
uint[2] fix;
```

Dynamic คือ Arrays ที่ไม่จำกัดขนาด

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

```c
struct Person {
  uint age;
  string name;
}

Person[] public people;
```

เราสามารถสร้าง Instance ของ Struct ได้แบบนี้

```js
Person aom = Person(20, "aomm");
```

> ซึ่ง Args ของ Person จะเรียงตาม Struct นั้นคือ 20 = age, aomm = name

เราสามารถเพิ่ม `aom` เข้าไปใน Arrays `people` ได้โดย

```js
people.push(aom) 
```

><เสริม> Arrays.push() จะ Return ค่า length ของ arrays ออกมา

### Private / Public Functions

ใน Solidity ฟังก์ชั่นจะมีค่า visible เริ่มต้น เป็น `public` ซึ่งทุกคนและทุก contract
สามารถเข้าถึงและเรียกใช้งานได้

`private` keyword จะทำให้ function ถูกเรียกใช้งานได้แค่ภายใน contract นี้เท่านั้น

การตั้ง visible เป็น `public` เพราะอาจทำให้ Contract ของเราโดนโจมตีได้
ดังนั้นเราจะกำหนดให้ฟังก์ชันเป็น `private` ทุกครั้งเป็นค่าเริ่มต้น

ตัวอย่างการประกาศฟังก์ชันแบบ `private`

```c
uint[] numbers;
function _addNumber(uint _num) private {
    numbers.push(_num);
}
```

>การประกาศ function ที่เป็น private มักจะใช้ชื่อที่นำหน้าด้วย underscore ( _ )

การประกาศ function แบบนี้หมายความว่า `function` ภายใน `contract` นี้เท่านั้นที่สามารถเรียกใช้ฟังก์ชันนี้ได้

### More on function

#### Return value

การส่งคืนค่าจาก function สามารถเขียนได้ดังนี้ ซึ่งจะมี Keyword คือ `returns` (เติม s ด้วยนะ)

```js
string greeting = "What's up dog";

function sayHello() public returns (string memory) {
  return greeting;
}
```

ใน Solidity การ Return ใน Function จะมีการกำหนด Data type ของข้อมูลที่จะ Return

ในตัวอย่างคือ `string`

> และอย่าลืม `string` เป็น Reference Type ต้องมี keyword `memory`

#### Function modifiers

จากตัวอย่างข้างต้น function จะไม่เปลี่ยนค่า/เขียนค่าลง `State` หรือสรุปก็คือเป็นการอ่านค่า `State`

ดังนั้นในกรณีนี้เราจะใช้ `Modifier` คือ `view` ไว้บอกว่า function นี้มีการยุ่งเกี่ยวกับค่าใน storage (`state`)

ตัวอย่าง

```js
string greeting = "What's up dog";

function sayHello() public view returns (string memory) {
  return greeting;
}
```

ใน solidity มี concept ของ [pure function](https://medium.com/@aonrobot/pure-function-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3-2e42784c9dae#:~:text=Pure%20Function%20%E0%B8%84%E0%B8%B7%E0%B8%AD%20%E0%B8%9F%E0%B8%B1%E0%B8%87%E0%B8%81%E0%B9%8C%E0%B8%8A%E0%B8%B1%E0%B8%99%E0%B8%97%E0%B8%B5%E0%B9%88,%E0%B8%82%E0%B8%AD%E0%B8%87%E0%B8%95%E0%B8%B1%E0%B8%A7%E0%B8%A1%E0%B8%B1%E0%B8%99%20%E0%B8%95%E0%B8%B1%E0%B8%A7%E0%B8%AD%E0%B8%A2%E0%B9%88%E0%B8%B2%E0%B8%87%E0%B9%80%E0%B8%8A%E0%B9%88%E0%B8%99)

ซึ่ง pure ฟังก์ชันคืออะไร อ่านได้จากบทความด้านบน

สรุปคือ pure function มีข้อกำหนดคือ

1. ข้อที่ 1
Pure Function คือ ฟังก์ชันที่ไม่ขึ้นอยู่กับค่าตัวแปรหรือไม่เปลี่ยนแปลงค่าตัวแปร (Variables) ที่อยู่นอก scope ของตัวมัน
ข้อที่ 2
2. Pure Function จะต้องสามารถคาดการณ์ (Predictability) ค่าที่จะ return ออกมาได้ จาก arguments ที่เราส่งเข้าไป หมายความว่าถ้าเราเรียกฟังก์ชั่นเดิมโดยส่งค่า arguments เข้าไปเหมือนเดิม ไม่ว่าจะเรียกฟังก์ชั่นนั้นกี่ครั้ง ค่าที่ return ออกมายังไงก็ต้องได้ค่าเหมือนเดิมทุกครั้ง

ถ้าเป็น pure function ใน solidity จะมี keyword ชื่อว่า `pure`

มาดูตัวอย่างกัน

```js
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
```

จะเห็นว่า function `_multiply` จะไม่ยุ่งเกี่ยวกับ `state` ค่าที่มันส่งกลับมาจะขึ้นอยู่กับ `params` ที่รับเข้าไป
ดังนั้นเราใส่ keyword `pure` เข้าไปปปป

### Keccak256 and Typecasting

#### Keccak256

ใน Ethereum มีฟังก์ชันในการทำ Hash อยู่ชื่อว่า `keccak256`
ซึ่งมันใช้ในหลายวัตถุประสงค์ใน Ethereum

ซึ่ง `function keccak256` จะรับ `parameters` ตัวเดียวเป็นชนิด `byte`

ตัวอย่างเช่น

```js
//6e91ec6b618bb462a4a6ee5aa2cb0e9cf30f7a052bb467b0ba58b8748c00d2e5
keccak256(abi.encodePacked("aaaab"));
//b1f078126895a1424524de5321b339ab00408010b7cf0e6ed451514981e58aa9
keccak256(abi.encodePacked("aaaac"));
```

> จะเห็นว่าแค่เปลี่ยนข้อมูลของ input นิดเดียวก็ทำให้ค่าออกมาเปลี่ยนแปลงไปจากเดิมเยอะมากกก

---
**หมายเหตุ**

การสร้างตัวเลขสุ่มที่ปลอดภัยในบล็อคเชนเป็นปัญหาที่ยากมาก อันนี้เป็นการยกตัวอย่าง `function`

---

#### Typecasting

การเปลี่ยนชนิดข้อมูลใน Solidity สามารถทำได้ดังนี้

```c
uint8 a = 5;
uint b = 6;
// error เพราะว่า a * b ให้ค่าเป็น unit ไม่ใช่ uint 8
uint8 c = a * b;
// เราสามารถแปลงให้ b เป็น uint8 ก่อนโดยการทำแบบนี้
// ค่าที่ได้จากการคูณกันจึงเป็น type uint8
uint8 c = a * uint8(b);
```
