# GetX 쓰는 이유
* State management
* 코드의 간결성

# GetX State management
* Simple State Manager with GetBuilder
* Reactive State Manager

# GetX Simple State manager
* GetX 패키지 설치 -> Controller 클래스 생성 -> GetXController 상속 -> Update 메서드 호출 -> Dependency Injection(Get.put) -> GetBuilder 호출 -> controller.x 또는 Get.find<controller> 사용
* 장점: Low cost
* 단점: Manually update
``` dart
// main.dart
import 'package:flutter/material.dart';
import 'package:practiceapp/controller.dart';
import 'package:get/get.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}


class MyHomePage extends StatelessWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Controller controller = Get.put(Controller()); // Controller class의 변수와 메서드에 접근하기 위해 Controller instance 생성

    return Scaffold(
      appBar: AppBar(
        title: Text('GetX'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            GetBuilder<Controller>( // <Controller> : controller instance 내의 데이터 사용 // GetBuilder : 변한 state를 화면에 다시 그려주는 역할
              init: Controller(), // 여기서도 controller instance 생성가능
              builder: (_) => Text(
                'Current value is: ${Get.find<Controller>().x}', // Get.find: GetBuilder 내에서 생성한 instance를 직접 찾아줌
                style: TextStyle(fontSize: 20, color: Colors.red),
              ),
            ),
            SizedBox(
              height: 20,
            ),
            ElevatedButton(
              onPressed: (){
                Get.find<Controller>().increment();
              },
              child: Text('Add number'),
            )
          ],
        ),
      ),
    );
  }
}
```
``` dart
// controller.dart
import 'package:get/get_state_manager/get_state_manager.dart';

class Controller extends GetxController{ // GetX로 state management하기 위해

  int _x = 0;
  int get x => _x; // 외부에서 이 값을 읽어오는 용도로만 사용하고 싶을 때

  void increment(){
    _x++;
    update(); // setState method와 비슷
  }
}
```



