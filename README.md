# SwiftUI笔记

## SwiftUI状态初始化

1. `@State`初始化

  ```swift
  struct CounterView: View {
      @State private var count: Int
      
      init(count: Int) {
          self.count = count
  
      }
      var body: some View {
          VStack {
              Text("Counter: \(count)")
              Button("+1") {
                  count += 1
              }
          }
      }
  }
  ```

  [参考链接](https://sarunw.com/posts/state-variable-initialization/)

2. `@StateObject`初始化

  ```swift
  /// 第一种
  class DashboardViewModel: ObservableObject {
      @Published var greeting: String
      
      init(name: String? = nil) {
          if let name = name {
              greeting = "Hello, \(name)!"
          } else {
              greeting = "Hello there"
          }
      }
      func update(name: String) { // 1
          greeting = "Hello, \(name)!"
      }
  }
  struct DashboardView: View {
      var user: User
      
      @StateObject var viewModel = DashboardViewModel()
      
      var body: some View {
          Text(viewModel.greeting)
              .padding()
              .onAppear {
                  viewModel.update(name: user.name) // 1
              }
          
      }
  }
  
  /// 第二种
  class DashboardViewModel: ObservableObject {
    @Published var greeting: String
     
    init(name: String) {
      greeting = "Hello, \(name)!"
    }
  }
  
  struct DashboardView: View {
    @StateObject private var viewModel: DashboardViewModel
     
    init(name: String) {
      _viewModel = StateObject(wrappedValue: DashboardViewModel(name: name))
    }
  
    var body: some View {
      Text("Greeting: \(viewModel.greeting)")
    }
  }
  ```

  [参考链接](https://sarunw.com/posts/how-to-initialize-stateobject-with-parameters-in-swiftui/)









