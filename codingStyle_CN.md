#  CodingStyle ver.2024.06.01

[TOC]

## 文件路径命名管理规范

- 文件名使用 `全大写文件类型英文缩写_英文简述小驼峰法.文件格式` 的形式命名
	- 例如 DOC_codingStyle.md 是一个合法的命名
	- 其中 `DOC` 表示这是一个文档类的文件
	- 其中 `codingStyle` 是文件的简述名称，使用小驼峰法命名
	- 其中 `.md` 表示这是一个 markdown 文件
- 文件夹名使用 `英文简述大驼峰法.文件格式` 的形式命名
- 当文件/文件夹之间具有层级关系时，可以使用 `.` 进行父子级之间的文件名标记
- 文件名、文件夹名中不允许出现除 `_`、`.`、`-` 以外的特殊字符，其他字符以 `-` 替换

每个具体项目中的文件路径存放管理规则依照对应仓库中的 README.md 中的 Developing Note 部分规定的内容执行。

## C/C++ 代码风格规范

### 命名规范

- 类名、结构名等自定义数据类型标识符使用大驼峰命名法，不允许包含下划线
```cpp
  class CustomerAccount {}; 			// 示例
```

- 变量名、函数名、命名空间名等标识符使用小驼峰命名法，可以用下划线分隔
```cpp
  int employeeCount; 					// 变量名示例
  void calculateTotal();  				// 函数名示例
  namespace myApplication {} 			// 命名空间名示例
```

- 常量名使用全大写、下划线分隔单词的命名规则
```cpp
  const double PI_5F = 3.14159; 		// 示例
```

- 宏定义名称使用全大写、下划线分割单词、以单个下划线开头和结尾的命名规则
```cpp
  # define _MY_APP_CONSTANT_ 1 			// 示例
```

- 函数的形式参数名使用以单个下划线开头的小驼峰命名法
```cpp
  void processItem(int _itemNumber); 	// 示例
```

### 空格、空行使用规范

#### 空格、换行符使用规范

- 统一使用四空格缩进，不使用制表符
- 如为保持缩进一致，允许引入多余空格，但应保证引入多余空格数量尽可能少
- `{` 的前一个字符不应该是 ` \n `，这是为了保证编辑器在显示当前块层级时能完整显示 `{` 之前的内容
- `#` 之后应该添加一个空格
- 不同的代码块之间应使用空行分隔，具体分隔规则见下文

#### 括号类运算符空格规则

- 用于作为计算表达式的括号类运算符外侧添加空格
- 关键字后的 `()` 应该用空格和关键字隔开
- 函数名后的 `()` 紧跟函数名，数组名后的 `[]` 紧跟数组名
- `<>` 外侧不添加空格，`<>`、`[]`、`()`内侧不直接添加空格
- 不省略 `{}`，但是可以把它写在同一行内，内外侧都添加空格

```cpp
/*
* @brief To figure out the first _len terms of fibonacci integer array.
* @param _len The length to figure out.
* @return The fibonacci integer array.
*/
vector<int> fibonacci(int _len) {
	vector<int> vec(_len);
	vec[0] = 0;
	vec[1] = 1;
	
	for (int i = 2; i < 16; i++) { vec[i] = vec[i - 1] + vec[i - 2]; }
	
	return vec;
}
```

#### 运算符添加空格规则

- `,`、`;` 后添加空格
- 双目运算符左右两侧添加空格
- 单目运算符外侧添加空格
- 三目运算符的每个运算符左右两侧添加空格
- `.`、`->`、`::` 运算符左右两侧无空格

#### 空行分隔代码块规则

- **全局变量声明与其他代码块之间**：间隔两个空行
  - 示例：
```cpp
    // 上一个代码块

    int num;
    int tot;
    float tot_score;
    float rate_score;
    bool flag;

    // 下一个代码块
```
- **不同种类的定义代码块之间**：间隔两个空行
  - 示例：
```cpp
	bool flag; 


    class templateClass {
        public:
            int id;
            int val;
        protected:
            queue<int> q;
    };

    
	inline int getSonNumber(templateClass _node) { return _node.val; }
```

- **同种定义代码块的不同的定义之间**：使用一个空行隔开
  - 示例：
```cpp
    inline int getSonNumber(templateClass _node) { return _node.val; }

    inline void insertSonCode(templateClass& _node, templateSonClass& _son) {
        _son.fa_id = _node.id;
        _node.val++;
        return;
    }
```

- **较复杂的代码块，不便于阅读的**：可以用单个空行将功能区划分开，以提高可读性
  - 示例：
```cpp
    void complexFunction() {
        // 复杂代码块开始
        // ...
        // 单个空行
        // 继续复杂代码块
    }
```

### 注释规范

- 函数和类的注释使用 `/* */` 方式进行多行注释，使用 Doxygen 注释风格的 `@` 指令详细解释其功能、参数、返回值等信息
- 行末 `//` 注释控制长度，同一个代码块内的行末注释保持缩进一致
- 行末注释仅允许用于类内成员变量声明、全局变量声明、函数声明等标识符声明定义处，不可用于函数内
- 在函数内为语句添加注释时，使用 `//` 在行间注释，用以说明注释处下方代码块作用
- 注释仅允许写在行间或行末，禁止在行内插入注释
- 所有注释部分应与注释符号中的 `/`、`*` 用一个空格隔开

```cpp
int targetNum;						// The number to be checked in fibonacci series.


vector<int> fibonacci(int _len);	// To figure out the first _len terms of fibonacci series.
int findInFibonacci(int _tgt);		// To figure out which term in fibonacci series is the given number.


/*
* @brief To figure out the first _len terms of fibonacci series.
* @param _len The length to figure out.
* @return The fibonacci integer array.
*/
vector<int> fibonacci(int _len) {
	vector<int> vec(_len);
	vec[0] = 0;
	vec[1] = 1;
	
	// Recursive computation of the Fibonacci series.
	for (int i = 2; i < _len; i++) {
		vec[i] = vec[i - 1] + vec[i - 2];
	}
	
	return vec;
}

/*
* @brief To figure out which term in fibonacci series is the given number.
* @param _tgt The number to be checked.
* @returns The index of the given number in fibonacci series.
* @returns -1 stands for not found.
*/
int findInFibonacci(int _tgt) {
	const vector<int> fib = fibonacci(50);
	for (int i = 0; i < 50; i++) {
		if (fib[i] == _tgt) return i;
		if (fib[i] > _tgt) return -1;
		if (fib[i] < 0) return -1;
	}
	return -1;
}
```

### 多文件项目编写规范

- 头文件以 `# ifndef _HEADER_NAME_H_` 开头，以 `# endif` 结尾，其中 `_HEADER_NAME_H_` 是仅在此头文件内被定义的宏，`HEADER_NAME` 可更换为头文件的名称
- 除 `main()` 以外，C++ 项目的所有函数必须被声明和定义于命名空间内
- 函数的声明和定义存放于不同的文件内（包括成员函数）
  - 函数声明于头文件内，函数定义于源文件内，头文件和源文件不要求一一对应
  - 函数的声明与定义不存放在同一个文件内，除非：
    - 模板函数的声明与定义在同一个头文件内同时书写
    - 内联函数的声明与定义在同一个头文件内同时书写
  - 若头文件与源文件互相对应，那么头文件 `header.h` 对应的函数定义源文件命名建议名称为 `headerFS.cpp`（FS 后缀为 Function Source 的缩写）






## C# 代码风格规范

### 命名规范

- 常量名使用全大写字母，单词间用下划线分隔
```csharp
  const double PI_5F = 3.14159; 				// 示例
```

- 函数名、变量名、数组名、命名空间名等标识符使用小驼峰命名法，可以用下划线分隔
```csharp
  public void CalculateTotal() {}			 	// 示例
  public bool flag;								// 示例
```

- 函数参数名和私有成员名使用小驼峰命名法，并以下划线开头
```csharp
  public void processItem(int _itemNumber) {} 	// 示例
  private void _getIndex(int _targetNumber) {}	// 示例
  private bool _flag;							// 示例
```

- 类名、结构名使用大驼峰命名法，不使用下划线
```csharp
  public class CustomerAccount {} 				// 示例
```

- 接口名使用大驼峰命名法，并且以大写字母 `I` 开头
```csharp
  public interface IDrawable {} 				// 示例
```

- 枚举名使用大驼峰命名法，枚举成员使用和常量相同的命名规范
```csharp
  public enum Alignment { LEFT, RIGHT, CENTER } // 示例
```

- 属性名使用小驼峰命名法
```csharp
  public int employeeCount { get; set; } 		// 示例
```

### 空格和空行使用规范

- 统一使用四空格缩进，不使用制表符
- `{` 的前一个字符不应该是 ` \n `，以确保编辑器能完整显示 `{` 之前的内容。
- 括号类运算符
	- 在 `()` 的外侧添加空格，内侧不添加
	- 当 `()` 紧跟函数名时，内外侧均不添加空格
	- `[]`、`<>` 的内外侧都不添加空格
	- `{}` 的内外侧均添加空格
```csharp
  if (condition) { } 			// 示例
  int[] array = new int[] { }; 	// 示例
```

- 在 `,`、 `;` 后添加空格，在双目运算符左右两侧添加空格，单目运算符外侧添加空格
```csharp
  int sum = a + b; 				// 示例
  int minusSum = ~sum + 1;		// 示例
```

- 不同代码块之间应使用若干数量的空行分隔
    - 函数的定义、类的定义等同种定义代码块之间用一个空行分隔
    - 不同种定义的代码块之间用两个空行分隔
```csharp
    int num;
    int tot;


    class MyClass {
        private _id;
        private _val;
        
        
		public int getId() {
            return _id;
        }
        
        public int getVal() {
            return _val;
        }
    }

	class SonClass : MyClass {}
```

### 注释规范

- 对函数的注释使用 `///` 进行 XML 文档注释，详细解释方法的功能、参数、返回值等信息
```csharp
  /// <summary>
  /// Calculates the total of a list of numbers.
  /// </summary>
  /// <param name="numbers">The list of numbers to calculate the total of.</param>
  /// <returns>The total of the numbers.</returns>
  public double CalculateTotal(List<double> numbers) {}
```

- 行末注释仅用于类内成员变量声明、全局变量声明、函数声明等标识符声明定义处，不可用于函数内
```csharp
  int targetNum; // The number to be checked in fibonacci series.
```

- 行间注释在函数内为语句添加注释时，使用 `//` 在行间注释，用以说明注释处下方代码块作用
```csharp
  // Check if the number is a fibonacci number
  if (isFibonacci(targetNum)) {
      // Perform some action
  }
```

- 注释仅允许写在行间或行末，禁止在行内插入注释。



## JavaScript 代码风格规范

### 命名规范

- 函数名使用小驼峰命名法
```javascript
  function calculateTotal() {} 	// 示例
```

- 变量名使用小驼峰命名法，以下划线开头的变量名表示私有变量
```javascript
  let _employeeCount = 0; 		// 私有变量示例
  let itemCount = 0;       		// 公共变量示例
```

- 常量名使用全大写字母，单词间用下划线分隔
```javascript
  const PI_5F = 3.14159; 		// 示例
```

- 类名使用大驼峰命名法，不使用下划线
```javascript
  class CustomerAccount {} 		// 示例
```

- 接口名使用大驼峰命名法，并以大写字母 `I` 开头
```javascript
  class IDrawable {} 			// 示例
```

- 函数参数名和私有成员名使用小驼峰命名法，并以下划线开头
```javascript
  function processItem(_itemNumber) {} 	// 示例
```

- 使用默认导出或具名导出时，遵循相应的命名约定
```javascript
  // 默认导出
  export default CustomerAccount;

  // 具名导出
  export { CustomerAccount, calculateTotal };
```

### 空格和空行使用规范

- 统一使用四空格缩进，不使用制表符
- 括号类运算符
  	- `()` 的外侧添加空格，内侧不添加空格
	- 当 `()` 紧跟函数名时，内外侧均不添加空格
	- `[]`  的内外侧都不添加空格
	- `{}` 的内外侧均添加空格
- 在 `,`、 `;` 后添加空格，在双目运算符左右两侧添加空格，单目运算符外侧添加空格
- 不同代码块之间应使用若干空行分隔
- 使用方法定义对象时，方法名和冒号之间不添加空格，方法体和括号之间也不添加空格
```javascript
  const person = {
      name() {},
      age: 30
  };
```
- `{` 前不应该是 ` \n ` 字符，以保证编辑器能完整显示 `{` 前的内容

### 注释规范

- 函数注释使用 JSDoc 注释风格，为函数提供详细的文档注释
```javascript
  /**
   * 计算数字列表的总和。
   * @param {Array} numbers - 需要计算总和的数字列表。
   * @return {number} 数字列表的总和。
   */
  function calculateTotal(numbers) {
      // ...
  }
```
- 行末注释使用 `//` ，控制长度，同一代码块内保持缩进一致
- 在函数内为语句添加注释时，使用 `//` 在行间注释，用来标记注释下方代码
```javascript
  // 检查数字是否是斐波那契数
  if (isFibonacci(targetNum)) {
      // 执行某些操作
  }
```
- 注释仅允许写在行间或行末，禁止在行内插入注释

### 其他规范

- 优先使用 `const` 声明只读变量，如果需要可重赋值的变量，则使用 `let`，最后才考虑使用 `var`
- 使用反引号（`` ` ``）来定义模板字符串
- 箭头函数的 `{}` 不省略
```javascript
  const sum = (num1, num2) => { num1 + num2; };
```
- 使用ES6模块化标准来组织代码，`import` 和 `export` 语句应简洁明了



## ShaderLab 代码风格规范

### 命名规范

- Shader名称使用全大写英文缩写和大驼峰法的组合形式命名
```shader
  Shader "MY_APP/MyCustomShader" {}
```

- 属性名使用大驼峰命名法，并以下划线开头
```shader
  Properties {
      _MainTex ("Texture", 2D) = "white" {}
      _Color ("Color", Color) = (1,1,1,1)
  }
```

- 自定义函数应使用小驼峰命名法
```shader
  float customFunction(float input) {
      return input * 2.0;
  }
```

### 空格和空行使用规范

- 统一使用四空格缩进，不使用制表符
- 使用两个空行分隔不同的代码块，如 Properties 和 SubShader 之间用两个空行分隔
- 不同 Pass 之间用一个空行隔开，不同 SubShader 之间用两个空行分隔

### 注释规范

- 行末注释使用 `//` ，控制长度，同一代码块内保持缩进一致
- 在函数内为语句添加注释时，使用 `//` 在行间注释，用来标记注释下方代码
- 注释仅允许写在行间或行末，禁止在行内插入注释
- 可以在函数的定义上方使用 `/* */` 添加多行注释来注释函数，但这并不是必须的

### ShaderLab特定规范

- **Properties块**：属性声明应优先按逻辑顺序排列，再按字典序排列，每个属性一行
- **SubShader和Pass**：清晰地定义 SubShader 和 Pass 块，不同 Pass 之间用空行隔开
- **CGPROGRAM 和 ENDCG**：包围着顶点和片段着色器代码的 CGPROGRAM 和 ENDCG 之间应保持空行
- 编写 Shader 代码时使用 Cg 语言并不是必须的

### 示例

```shader
// 版权声明和Shader描述
Shader "MY_APP/MyCustomShader" {
    Properties {
        _MainTex ("Albedo (RGB)", 2D) = "white" {}
        _Color ("Color", Color) = (1,1,1,1)
    }
    
    
    SubShader {
        Tags { "RenderType"="Opaque" }
        LOD 200
        
        Pass {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #include "UnityCG.cginc"
            
            // 顶点着色器
            struct appdata {
                float4 vertex : POSITION;
                float2 uv : TEXCOORD0;
            };
            
            // 片段着色器输入结构
            struct v2f {
                float2 uv : TEXCOORD0;
                float4 vertex : SV_POSITION;
            };
            
            v2f vert (appdata v) {
                v2f o;
                o.vertex = UnityObjectToClipPos(v.vertex);
                o.uv = v.uv;
                return o;
            }
            
            fixed4 frag (v2f i) : SV_Target {
                fixed4 col = tex2D(_MainTex, i.uv) * _Color;
                return col;
            }
            ENDCG
        }
    }
    
    
    // 其他SubShader或Pass块可以继续添加
}