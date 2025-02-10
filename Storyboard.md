macOS 앱 개발에서도 Storyboard를 사용할 수 있습니다.
 Xcode에서 macOS 프로젝트를 생성할 때 기본적으로 Storyboard 기반의 인터페이스가 설정됩니다.
 하지만 iOS와는 몇 가지 차이점이 있습니다.

1. macOS에서 Storyboard 사용 가능 여부
Xcode에서 macOS 앱을 만들 때 AppKit 기반의 Storyboard 또는 XIB를 사용할 수 있습니다.
macOS Storyboard는 iOS Storyboard와 다소 차이가 있음 (예: NSViewController, NSWindowController 사용).
SwiftUI의 등장 이후, Storyboard 대신 SwiftUI를 사용하는 것도 가능하지만, 기존 프로젝트에서는 여전히 Storyboard를 많이 사용합니다.

2. macOS에서 Storyboard 구조
macOS의 Storyboard는 iOS와 달리 **윈도우(NSWindow)와 뷰 컨트롤러(NSViewController)**를 관리하는 방식이 다릅니다.
표는 추후 예정


3. macOS에서 Storyboard 프로젝트 설정 방법
1️⃣ macOS 프로젝트 생성
Xcode에서 macOS App 프로젝트 생성 (AppKit 기반).
Main.storyboard가 기본으로 생성됨.
AppDelegate.swift와 SceneDelegate.swift 없이 AppKit의 NSApplicationDelegate가 기본 포함됨.
2️⃣ Storyboard 구조
NSWindowController: 윈도우를 관리하는 컨트롤러.
NSViewController: 개별 화면을 관리.
Segue: 화면 전환(Show, Modal 등 지원).

4. macOS에서 Storyboard 사용 예제
🔹 기본적인 Storyboard 연결
기본적으로 Main.storyboard 안에는 NSWindowController가 있으며,
 이를 AppDelegate.swift에서 연결해야 합니다.

1️⃣ AppDelegate.swift 설정


    
import Cocoa

 @main
 class AppDelegate: NSObject, NSApplicationDelegate {
    var window: NSWindow?
    func applicationDidFinishLaunching(_ aNotification: Notification) {
        // 스토리보드에서 윈도우 로드
        let storyboard = NSStoryboard(name: "Main", bundle: nil)
        if let mainWindowController = storyboard.instantiateController(withIdentifier: "MainWindowController") as? NSWindowController {
            window = mainWindowController.window
            window?.makeKeyAndOrderFront(nil)
        }
    }
 }

NSStoryboard(name: "Main", bundle: nil)을 사용해 Storyboard에서 NSWindowController를 로드.
instantiateController(withIdentifier:)를 통해 Storyboard에서 특정 컨트롤러를 가져옴.
2️⃣ Storyboard에서 Identifier 설정
Main.storyboard에서 NSWindowController 선택.
오른쪽 속성 창에서 Storyboard ID를 MainWindowController로 설정.

5. macOS에서 Storyboard의 한계
❌ 네비게이션 컨트롤러 없음
iOS의 UINavigationController처럼 자동으로 화면을 관리하는 기능이 없음.
대신 NSViewController를 수동으로 관리해야 함.
❌ iOS보다 제한적인 Segue 지원
Push 대신 Show 및 Modal 방식이 주로 사용됨.
Present as Sheet (iOS의 modal과 비슷한 개념) 방식이 일반적.

6. macOS에서 Storyboard vs. SwiftUI
표 추후 예정

✅ Storyboards는 기존 macOS AppKit 프로젝트에서 계속 사용되며, 기존 XIB 기반 프로젝트보다 관리가 편리합니다.
 ✅ SwiftUI는 macOS 11 이상에서 Storyboard 없이 UI를 구축하는 최신 방식입니다.

7. 결론
MacOS에서 Storyboard를 사용할 수 있음 (NSWindowController, NSViewController 기반).
iOS와 다르게 네비게이션 컨트롤러가 없고, 화면 전환을 직접 관리해야 함.
Storyboard를 활용하면 XIB보다 효율적이지만, 최신 macOS 개발에서는 SwiftUI로 전환하는 것이 권장됨.


