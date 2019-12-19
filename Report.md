# รายงานผลการทดลอง

<อุทัยพันธ์  เที่ยงโคตร> <603410073-5>

## คำสั่งการแสดงผลผ่าน Logcat

Debug log

```kotlin
Log.d(String, String)
```

Error log

```kotlin
Log.e(String, String)
```

Info log

```kotlin
Log.i(String, String)
```

Verbose log

```kotlin
Log.v(String, String)
```

Warning log

```kotlin
Log.w(String, String)
```

## SNACKBAR และ TOST

คำสั่งแสดง Snackbar

```kotlin
Snackbar.make(view, stringId, duration).show()

EX
Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
    .setAction("Action", null).show()
```

คำสั่งแสดง Tost

```kotlin
Toast.makeText(context, text, duration).show()

EX
Toast.makeText(this,"Replace with your own action",Toast.LENGTH_LONG).show()
```

## Android LiveCycle Activity

จงอธิบาการทำงานของเมธอทต่อไปนี้ ว่าเกิดขึ้นเมื่อใดของโปรแกรม พร้อมแสดงตัวอย่างโค้ดการทำงานของเมธอท (กำหนดให้แสดง log message เมื่อมีการทำงานของเมธอท)

1. onCreate() ->

```kotlin
onCreate() เป็นเมธอทแรกที่ทำงานเมื่อมีการเรียกใช้หน้า Activity นั้นๆ
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main2)
        Log.i("onCreate","Activity create") //โค้ดแสดง log message เมื่อฟังชั่นทำงาน
    }

```

2. onStart() ->

```kotlin
หลังจาก onCreate() ถูกเรียก onStart() ก็จะถูกเรียกตามมา ถ้าหาก Application ของเราถูกสั่งให้ไปอยู่ใน Background 
(อาจจะโดยการสั่ง Launch Application อื่น เหนือ Application ของเรา) onStart() จะถูกเรียกเมื่อเรากลับมาที่ Application อีกครั้ง
override fun onStart(){
        super.onStart()
        Log.i("onStart","Activity Start") //โค้ดแสดง log message เมื่อฟังชั่นทำงาน
    }
```

3. onResume() ->

```kotlin
onResume() จะทำงานเมื่อกลับมายังหน้าเดิมเช่นการกดปุ่มย้อนกลับเพราะ Activity ยังไม่ถูกปิดแต่ถูกซ่อนไว้หลังจากที่เรียก Activity อื่นขึ้นมา
override fun onResume(){
        super.onResume()
        Log.i("onResume","Activity Resume") //โค้ดแสดง log message เมื่อฟังชั่นทำงาน
    }
```

4. onPause() ->

```kotlin
onPause() จะทำงานเมื่อมีการเรียก Activity อื่นขึ้นมา จะทำให้ Activity เดิมทำการเรียกเมธอท onPause() เพื่อหยุดการทำงานไว้ชั่วขณะและ hidden
override fun onPause(){
        super.onPause()
        Log.i("onPause","Activity Pause") //โค้ดแสดง log message เมื่อฟังชั่นทำงาน
    }
```

5. onStop() ->

```kotlin
onStop() จะถูกเรียกเมื่อ Activity ออกจาก Screen เรียบร้อยแล้ว หรือเมื่อเราเปลี่ยนไป Interact กับอีก Activity หนึ่งแทน (เปลี่ยนจากสถานะ Active ไปเป็น Inactive) แต่นี่ไม่ได้หมายความ Activity ถูกปิดตัวลง เพียงแค่เปลี่ยนมาอยู่ในสถานะ Inactive ถ้าหากเรามีการประมวลผลใดที่ต้องการ Run เฉพาะตอนที่ Active นี่คือ Method ที่เหมาะสมที่เราจะสั่งหยุดการประมวลผลดังกล่าว
override fun onStop(){
        super.onStop()
        Log.i("onStop","Activity Stop") //โค้ดแสดง log message เมื่อฟังชั่นทำงาน
    }
```

6. onDestroy() ->

```kotlin
onDestroy() เป็น method สุดท้ายที่จะถูกเรียก ก่อนที่ Activity จะปิดตัวลงอย่างถาวร เป็น Method ที่เราใช้ในการคืนค่า resources หรือ clean up ใดๆ ก่อนที่ Activity จะถูกเก็บกวาดด้วย Garbage Collector ภายใน Method นี้ เราควรจะสั่งปิด Process ใดๆที่เราสั่ง Run ไว้ใน Background
override fun onDestroy(){
        super.onDestroy()
        Log.i("onDestroy","Activity Destroy") //โค้ดแสดง log message เมื่อฟังชั่นทำงาน
    }
```

7. onRestart() ->

```kotlin
onRestart() จะทำงานหลังจาก onStop () เมื่อ Activity กำลังถูกแสดงอีกครั้ง (มีการเรียก Activity เดิม) ก็เรียก onStart () และจากนั้น onResume ()
override fun onRestart(){
        super.onRestart()
        Log.i("onRestart","Activity Restart") //โค้ดแสดง log message เมื่อฟังชั่นทำงาน
    }
```

## Start new Activity

คำสั่งสำหรับเปิด activity ใหม่

```kotlin
var i = Intent(this,Main2Activity::class.java)
startActivity(i)
```

คำสั่งสำหรับเปิด activity ใหม่ ผ่านเมนู setting

```kotlin
R.id.action_settings -> {
        var i = Intent(this,Main2Activity::class.java)
        startActivity(i)
        return true
    }
```
## CR
```kotlin
https://medium.com/sathittham/android-activity-life-cycle-%E0%B8%A7%E0%B8%87%E0%B8%88%E0%B8%A3%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%97%E0%B8%B3%E0%B8%87%E0%B8%B2%E0%B8%99%E0%B8%82%E0%B8%AD%E0%B8%87%E0%B9%81%E0%B8%AD%E0%B8%84%E0%B8%97%E0%B8%B4%E0%B8%A7%E0%B8%B4%E0%B8%95%E0%B8%B5%E0%B9%89-d19874e6d11e


https://developer.android.com/reference/android/app/Activity.html
```
