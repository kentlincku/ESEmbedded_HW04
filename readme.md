HW04
===
This is the hw04 sample. Please follow the steps below.

# Build the Sample Program

1. Fork this repo to your own github account.

2. Clone the repo that you just forked.

3. Under the hw04 dir, use:

	* `make` to build.

	* `make flash` to flash the binary file into your STM32F4 device.

	* `make clean` to clean the ouput files.

# Build Your Own Program

1. Edit or add files if you need to.

2. Make and run like the steps above.

3. Please avoid using hardware dependent C standard library functions like `printf`, `malloc`, etc.

# HW04 Requirements

1. Please practice to reference the user manuals mentioned in [Lecture 04], and try to use the user button (the blue one on the STM32F4DISCOVERY board).

2. After reset, the device starts to wait until the user button has been pressed, and then starts to blink the blue led forever.

3. Try to define a macro function `READ_BIT(addr, bit)` in reg.h for reading the value of the user button.

4. Push your repo to your github. (Use .gitignore to exclude the output files like object files, executable files, or binary files)

5. The TAs will clone your repo, build from your source code, and flash to see the result.

[Lecture 04]: http://www.nc.es.ncku.edu.tw/course/embedded/04/

--------------------

- [] **If you volunteer to give the presentation (demo) next week, check this.**

--------------------

Take your note here if you want. (Optional)
HW04
===
## 1. 實驗題目
定義`READ_BIT(addr, bit)`並實作出使用userpin控制LED燈。
## 2. 實驗步驟
1. 定義`#define READ_BIT(addr, bit) ((REG(addr) & (UINT32_1 << (bit))))`於reg.h中
由`00000001 & addr`可以找出要測試位置的值

2. 修改blink.c檔案，由使用手冊中可以看到userpin的腳位是PA0，在初始化PA0時，需要將mode改為input，並且修改PUPDR為10


```
	SET_BIT(RCC_BASE + RCC_AHB1ENR_OFFSET, GPIO_EN_BIT(GPIO_PORTA));
	CLEAR_BIT(GPIO_BASE(GPIO_PORTA) + GPIOx_MODER_OFFSET, 1);
	CLEAR_BIT(GPIO_BASE(GPIO_PORTA) + GPIOx_MODER_OFFSET, 0);
	SET_BIT(GPIO_BASE(GPIO_PORTA) + GPIOx_PUPDR_OFFSET, 1);
	CLEAR_BIT(GPIO_BASE(GPIO_PORTA) + GPIOx_PUPDR_OFFSET, 0);
```
![](https://github.com/kentlincku/ESEmbedded_HW04/blob/master/reg.png)
![](https://github.com/kentlincku/ESEmbedded_HW04/blob/master/code.png)


