# DevelopmentSpecification ver. 2024.06.04

[TOC]

## Table of Contents

## File Path Naming Management Specification

- File names should be in the format of `ALL_CAPS_FILE_TYPE_ABBREVIATION_lowerCamelCase.FORMAT`
  - For example, `DOC_codingStyle.md` is a valid name
  - Where `DOC` indicates that it is a document type file
  - `codingStyle` is a brief name for the file, using lower camel case naming
  - `.md` indicates that it is a markdown file

- Folder names should be in the format of `lowerCamelCaseAbbreviation.FORMAT`

- When there is a hierarchical relationship between files/folders, a `.` can be used to mark parent-child file names

- File names and folder names should not contain special characters other than `_`, `.`, `-`. Replace other characters with `-`

- The file path storage management rules for each specific project should follow the content of the "Developing Note" section in the corresponding repository's `README.md`



## General Documentation Comment Standards for Code

- At the beginning of the code, there should be multi-line document comments, including:
  - **@Description**: A brief description of the code content.
  - **@Author**: The author who created the code.
  - **@Email**: The email of the author who created the code.
  - **@Date**: The date when the code was created.
  - **@LastEditors**: The last contributor(s) to the code (same as the GitHub ID).
  - **@LastEditTime**: The last time the code was modified.
- Before functions, there should be multi-line document comments, including at least:
  - **@brief**: A brief description of the function's purpose.
  - **@param**: Comments on the function's parameters.
  - **@return**: Comments on the function's return value.
- In code files with multiple contributors, author comments can be added before functions and classes, which may include:
  - **@author**: The creator of the function/class.
  - **@email**: The email of the creator of the function/class.
- Document comments before classes are not mandatory, but detailed comments are required for class members.

Contributors who use Visual Studio Code for development are recommended to use the plugin [koroFileHeader](https://github.com/OBKoro1/koro1FileHeader) to add documentation comments.



## C/C++ Coding Style Specification

### Naming Conventions

- Class names, structure names, and other custom data type identifiers use PascalCase naming conventions and do not contain underscores
```cpp
  class CustomerAccount {};             // Example
```

- Variable names, function names, namespace names, and other identifiers use lower camel case naming conventions and can be separated by underscores
```cpp
  int employeeCount;                    // Variable name example
  void calculateTotal();                // Function name example
  namespace myApplication {}            // Namespace name example
```

- Constant names use all uppercase letters and words separated by underscores naming conventions
```cpp
  const double PI_5F = 3.14159;         // Example
```

- Macro definition names use all uppercase letters, words separated by underscores, and start and end with a single underscore naming conventions
```cpp
  #define _MY_APP_CONSTANT_ 1          // Example
```

- Function parameter names use lower camel case naming conventions starting with a single underscore
```cpp
  void processItem(int _itemNumber);    // Example
```

### Whitespace and Line Break Usage Specification

- Uniformly use four spaces for indentation, do not use tabs

- If extra spaces are introduced to maintain consistent indentation, ensure that the number of extra spaces is kept to a minimum

- The character before `{` should not be `\n`, to ensure that the editor can fully display the content before `{` when displaying the current block level

- A space should be added after `#`

- Different code blocks should be separated by a blank line, specific separation rules are described below

### Bracket Operator Whitespace Rules

- Add spaces on the outside of bracket operators used as expressions

- A space should separate keywords from `()` following the keyword

- The function name should be followed immediately by `()`, and the array name should be followed immediately by `[]`

- Do not add spaces on the outside of `<>`, and do not directly add spaces on the inside of `<>`, `[]`, `()`

- Do not omit `{}`, but they can be written on the same line with spaces added to the inside and outside

```cpp
/* 
 * @brief To figure out the first _len terms of fibonacci integer array.
 * @param _len The length to figure out.
 * @return The fibonacci integer array.
 */
vector fibonacci(int _len) {
    vector vec(_len);
    vec[0] = 0;
    vec[1] = 1;
}
```

### Operator Whitespace Rules

- Add spaces after `,`, `;`

- Add spaces on both sides of binary operators

- Add spaces on the outside of unary operators

- Add spaces on both sides of each of the operators in a ternary operator

- No spaces on both sides of `.`, `->`, `::` operators

### Blank Line Separation of Code Blocks Rules

- Global variable declarations and other code blocks: separated by two blank lines

- Example:
```cpp
    // Previous code block
    int num;
    int tot;
    float tot_score;
    float rate_score;
    bool flag;
    // Next code block
```

- Different types of definition code blocks: separated by two blank lines

  - Example: cpp
```cpp
    bool flag; 
    class templateClass {
        public:
            int id;
            int val;
        protected:
            queue q;
    };
    inline int getSonNumber(templateClass _node) { return _node.val; }
```

- Different definitions within the same type of definition code block: separated by one blank line

  - Example:
```cpp
    inline int getSonNumber(templateClass _node) { return _node.val; }
    inline void insertSonCode(templateClass& _node, templateSonClass& _son) {
        _son.fa_id = _node.id;
        _node.val++;
        return;
    }
```

- For more complex code blocks that are not easy to read: a single blank line can be used to divide functional areas to improve readability

  - Example: cpp
```cpp
    void complexFunction() {
        // Start of complex code block
        // ...
        // Single blank line
        // Continue with complex code block
    }
```

### Commenting Specification

- Function and class comments use `/* */` for multi-line comments, using Doxygen commenting style `@` directive to explain in detail its functionality, parameters, return values, and other information

- End-of-line `//` comments control the length, and end-of-line comments within the same code block maintain consistent indentation

- End-of-line comments are only allowed for class member variable declarations, global variable declarations, function declarations, and other identifier declarations and definitions, and should not be used inside functions

- When adding comments for statements inside a function, use `//` for in-line comments to explain the code block below the comment

- Comments are only allowed at the end of lines or in between lines, and in-line comment insertion is prohibited

- All comment parts should be separated by a space from the comment symbols `/` and `*`

```cpp
int targetNum;                      // The number to be checked in the fibonacci series.


vector<int> fibonacci(int _len);    // To figure out the first _len terms of the fibonacci series.
int findInFibonacci(int _tgt);      // To figure out which term in the fibonacci series is the given number.


/* 
 * @brief To figure out the first _len terms of the fibonacci series.
 * @param _len The length to figure out.
 * @return The fibonacci integer array.
 */
vector<int> fibonacci(int _len) {
    vector vec(_len);
    vec[0] = 0;
    vec[1] = 1;
    
    for (int i = 2; i < _len; i++) {
        vec[i] = vec[i - 1] + vec[i - 2];
    }
    
    return vec;
}

/* 
 * @brief To figure out which term in the fibonacci series is the given number.
 * @param _tgt The number to be checked.
 * @returns The index of the given number in the fibonacci series.
 * @returns -1 stands for not found.
 */
int findInFibonacci(int _tgt) {
    const vector fib = fibonacci(50);
    for (int i = 0; i < 50; i++) {
        if (fib[i] == _tgt) return i;
        if (fib[i] > _tgt) return -1;
        if (fib[i] < 0) return -1;
    }
    return -1;
}
```

### Multi-file Project Writing Specification

- Header files should start with `# ifndef _HEADER_NAME_H_` and end with `# endif`, where `_HEADER_NAME_H_` is a macro defined only within this header file, and `HEADER_NAME` can be replaced with the name of the header file

- Except for `main()`, all functions in the C++ project must be declared and defined within a namespace

- Function declarations and definitions are stored in different files (including member functions)

- Function declarations are in header files, and function definitions are in source files, and there is no requirement for header files and source files to correspond one-to-one

- Function declarations and definitions are not stored in the same file unless:

  - Template function declarations and definitions are written in the same header file at the same time

  - Inline function declarations and definitions are written in the same header file at the same time

- If the header file and source file correspond to each other, then the function definition source file corresponding to the header file `header.h` is recommended to be named `headerFS.cpp` (FS suffix stands for Function Source abbreviation)

## C# Coding Style Specification

### Naming Conventions

- Constant names use all uppercase letters, words are separated by underscores
```csharp
  const double PI_5F = 3.14159;                 // Example
```

- Function names, variable names, array names, namespace names, and other identifiers use lower camel case naming conventions and can be separated by underscores
```csharp
  public void CalculateTotal() {}               // Example
  public bool flag;                             // Example
```

- Function parameter names and private member names use lower camel case naming conventions and start with an underscore
```csharp
  public void processItem(int _itemNumber) {}   // Example
  private void _getIndex(int _targetNumber) {}  // Example
  private bool _flag;                           // Example
```

- Class and structure names use PascalCase naming conventions and do not contain underscores
```csharp
  public class CustomerAccount {}               // Example
```

- Interface names use PascalCase naming conventions and start with the uppercase letter I
```csharp
  public interface IDrawable {}                 // Example
```

- Enum names use PascalCase naming conventions, and enum members use the same naming conventions as constants
```csharp
  public enum Alignment { LEFT, RIGHT, CENTER } // Example
```

- Property names use lower camel case naming conventions
```csharp
  public int employeeCount { get; set; }        // Example
```

### Whitespace and Line Break Usage Specification

- Uniformly use four spaces for indentation, do not use tabs

- The character before `{` should not be ` \n ` to ensure that the editor can fully display the content before `{` when displaying the current block level.

### Bracket Operator

- Add spaces on the outside of `()`, do not add spaces on the inside

- When `()` immediately follows a function name, do not add spaces on the inside or outside

- Do not add spaces on the inside or outside of `[]`, `<>`

- Add spaces on both the inside and outside of `{}`

```csharp
  if (condition) { }            // Example
  int[] array = new int[] { };  // Example
```

- Add spaces after `,`, `;`, add spaces on both sides of binary operators, add spaces on the outside of unary operators

```csharp
  int sum = a + b;              // Example
  int minusSum = ~sum + 1;      // Example
```

- Different code blocks should be separated by a certain number of blank lines

- Between function definitions, class definitions, and other similar definition code blocks, use one blank line to separate

- Between different types of definition code blocks, use two blank lines to separate

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

### Commenting Specification

- Function comments use `///` for XML documentation comments, explaining in detail the functionality, parameters, return values, and other information of the method

```csharp
  /// <summary>
  /// Calculates the total of a list of numbers.
  /// </summary>
  /// <param name="numbers">The list of numbers to calculate the total of.</param>
  /// <returns>The total of the numbers.</returns>
  public double CalculateTotal(List<double> numbers) {}
```

- End-of-line comments use `//`, control the length, and maintain consistent indentation within the same code block

- End-of-line comments are only used for class member variable declarations, global variable declarations, function declarations, and other identifier declarations and definitions, and should not be used inside functions

- When adding comments for statements inside a function, use `//` for in-line comments to explain the code block below the comment

```csharp
  int targetNum; 				// The number to be checked in the fibonacci series.
  
  // Check if the number is a fibonacci number
  if (isFibonacci(targetNum)) {
      // Perform some action
  }
```

- Comments are only allowed at the end of lines or in between lines, and in-line comment insertion is prohibited

## JavaScript Coding Style Specification

### Naming Conventions

- Function names use lower camel case naming conventions
```javascript
  function calculateTotal() {}  // Example
```

- Variable names use lower camel case naming conventions, and variable names starting with an underscore indicate private variables
```javascript
  let _employeeCount = 0;       // Private variable example
  let itemCount = 0;            // Public variable example
```

- Constant names use all uppercase letters, and words are separated by underscores
```javascript
  const PI_5F = 3.14159;        // Example
```

- Class names use PascalCase naming conventions and do not contain underscores
```javascript
  class CustomerAccount {}      // Example
```

- Interface names use PascalCase naming conventions and start with the uppercase letter I
```javascript
  class IDrawable {}            // Example
```

- Function parameter names and private member names use lower camel case naming conventions and start with an underscore
```javascript
  function processItem(_itemNumber) {}  // Example
```

- When using default export or named export, follow the corresponding naming conventions
```javascript
  // Default export
  export default CustomerAccount;
  
  // Named export
  export { CustomerAccount, calculateTotal };
```

### Whitespace and Line Break Usage Specification

- Uniformly use four spaces for indentation, do not use tabs

- Bracket operators
  - Add spaces on the outside of `()`, do not add spaces on the inside
  - When `()` immediately follows a function name, do not add spaces on the inside or outside
  - Do not add spaces on the inside or outside of `[]`
  - Add spaces on both the inside and outside of `{}`

- Add spaces after `,`, `;`, add spaces on both sides of binary operators, add spaces on the outside of unary operators

- Different code blocks should be separated by a certain number of blank lines

- When defining objects using methods, do not add spaces between method names and colons, and do not add spaces between method bodies and parentheses

```javascript
  const person = {
      name() {},
      age: 30
  };
```

- The character before `{` should not be `\n` to ensure that the editor can fully display the content before `{`

### Commenting Specification

- Function comments use the JSDoc comment style to provide detailed documentation for functions

```javascript
  /**
  Calculate the sum of a list of numbers.
  
  @param {Array} numbers - The list of numbers to calculate the sum of.
  
  @return {number} The sum of the numbers.
  */
  function calculateTotal(numbers) {
      // ...
  }
```

- End-of-line comments use `//`, control the length, and maintain consistent indentation within the same code block

- When adding comments for statements inside a function, use `//` for in-line comments to mark the code below the comment

```javascript
  // Check if the number is a fibonacci number
  if (isFibonacci(targetNum)) {
      // Perform some actions
  }
```

- Comments are only allowed at the end of lines or in between lines, and in-line comment insertion is prohibited

### Other Specifications

- Prefer to declare read-only variables with `const`, if you need reassignable variables, use `let`, and consider using `var` as a last resort

- Use backticks (`` ` ``) to define template strings

- Do not omit `{}` in arrow functions

```javascript
  const sum = (num1, num2) => { return num1 + num2; };
```

- Use ES6 module standards to organize code, `import` and `export` statements should be concise and clear




## ShaderLab Code Style Specification

### Naming Conventions

- Shader names should be named using a combination of uppercase English abbreviations and CamelCase notation.
- Shader properties should use CamelCase notation and start with an underscore.
- Custom functions should use CamelCase notation.
- All custom variable names use the little camel nomenclature that does not begin with an underscore.

```shader
Shader "MY_APP/MyCustomShader" {
    Properties {
        _MainTex ("Texture", 2D) = "white" {}
        _Color ("Color", Color) = (1,1,1,1)
    }
}
float customFunction(float input) {
    return input * 2.0;
}
```

### Whitespace and Line Break Usage

- Use four spaces for indentation, do not use tabs.
- The character before `{` should not be ` \n ` to ensure that the editor can fully display the content before `{`.
- Use two blank lines to separate different code blocks, such as between Properties and SubShader.
- Use one blank line to separate different Passes, and two blank lines to separate different SubShaders.

### Commenting Conventions

- End-of-line comments should use `//`, control the length, and maintain consistent indentation within the same code block.
- In functions, add comments to lines using `//` to explain the code block below the comment.
- Comments are only allowed in between lines or at the end of lines; in-line comments are prohibited.
- You can add multi-line comments above the function definition using `/* */` to comment on the function, but this is not required.

### ShaderLab Specific Conventions

- Properties block: Property declarations should be arranged in logical order first, then in dictionary order, with one property per line.
- SubShader and Pass: Clearly define SubShader and Pass blocks, with blank lines separating different Passes.
- CGPROGRAM and ENDCG: Maintain blank lines between CGPROGRAM and ENDCG surrounding vertex and fragment shader code.
- When writing Shader code, using the Cg language is not required.

### Example:
```shader
// Copyright notice and shader description
Shader "MY_APP/MyCustomShader" {
    Properties {
        _MainTex ("Albedo (RGB)", 2D) = "white" {}
        _Color ("Color", Color) = (1,1,1,1)
    }
    
    
    SubShader {
        Tags { "RenderType"="Opaque" }
        LOD 100
        
        Pass {
            CGPROGRAM
            
            #pragma vertex vert
            #pragma fragment frag
            #include "UnityCG.cginc"
            
            struct appdata {
                float4 vertex : POSITION;
                float2 uv : TEXCOORD0;
            };
            
            struct v2f {
                float2 uv : TEXCOORD0;
                float4 vertex : SV_POSITION;
            };
            
            sampler2D _MainTex;
            float4 _Color;
            
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
    
    
    FallBack "Diffuse"
}
```