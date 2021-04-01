## 使用C语言的七个步骤

- 定义程序目标
- 设计程序
- 编写代码
- 编译
- 运行程序
- 测试和调试程序
- 维护和修改程序





## 常用库函数学习

### `stdio.h`

### `string.h`

### `limits.h`

提供了与整数类型大小限制的信息

```c

void test02()
{
	printf("打印limits.h头文件中一些明示的常量: \n");
	printf("CHAR_BIT = %d", CHAR_BIT);
	printf("\nCHAR_MAX = %d", CHAR_MAX);
	printf("\nSCHAR_MAX = %d", SCHAR_MIN);
	printf("\nSCHAR_MAX = %d", SCHAR_MAX);
	printf("\nUCHAR_MAX = %d", UCHAR_MAX);
	printf("\n");
	printf("\nSHRT_MAX = %d", SHRT_MAX);
	printf("\nSHRT_MIN = %d", SHRT_MIN);
	printf("\nUSHRT_MAX = %d", USHRT_MAX);
	printf("\nINT_MAX = %d", INT_MAX);
	printf("\nINT_MIN = %d", INT_MIN);
	printf("\nUINT_MAX = %d", UINT_MAX);
	printf("\n");
	printf("\nLONG_MAX = %d", LONG_MAX);
	printf("\nLONG_MIN = %d", LONG_MIN);
	printf("\nULONG_MAX = %d",ULONG_MAX);
	printf("\nLLONG_MAX = %lld", LLONG_MAX);
	printf("\nLLONG_MIN = %lld", LLONG_MIN);
	printf("\nULLONG_MAX = %llu", ULLONG_MAX);
}
// =========================打印结果=============================
/**
打印limits.h头文件中一些明示的常量:
CHAR_BIT = 8
CHAR_MAX = 127
SCHAR_MAX = -128
SCHAR_MAX = 127
UCHAR_MAX = 255

SHRT_MAX = 32767
SHRT_MIN = -32768
USHRT_MAX = 65535
INT_MAX = 2147483647
INT_MIN = -2147483648
UINT_MAX = -1

LONG_MAX = 2147483647
LONG_MIN = -2147483648
ULONG_MAX = -1
LLONG_MAX = 9223372036854775807
LLONG_MIN = -9223372036854775808
ULLONG_MAX = 18446744073709551615
*/
```



### `float.h`

提供了和浮点类型大小限制的信息

```c
void test03()
{
	printf("打印float.h头文件中浮点类型明示的常量: \n");
	printf("\nFLT_MANT_DIG = %f", FLT_MANT_DIG);
	printf("\nFLT_DIG = %f", FLT_DIG);
	printf("\nFLT_MIN_10_EXP = %f", FLT_MIN_10_EXP);
	printf("\nFLT_MAX_10_EXP = %f", FLT_MAX_10_EXP);
	printf("\nFLT_MIN = %f", FLT_MIN);
	printf("\nFLT_MAX = %f", FLT_MAX);
	printf("\nFLT_EPSILON = %f", FLT_EPSILON);
}
// =========================打印结果=============================
/**
打印float.h头文件中浮点类型明示的常量:
FLT_MANT_DIG = 0.000000
FLT_DIG = 0.000000
FLT_MIN_10_EXP = 0.000000
FLT_MAX_10_EXP = 0.000000
FLT_MIN = 0.000000
FLT_MAX = 340282346638528859811704183484516925440.000000
FLT_EPSILON = 0.000000
*/

```

