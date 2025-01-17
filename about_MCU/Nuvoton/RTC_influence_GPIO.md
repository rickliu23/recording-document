# 问题描述

+ MCU型号：M467JJHAN
+ 装纽扣电池的前提下，设备重启之后，部分SPI工作受影响，无法输入、输出数据
  + 受影响的SPI引脚：PF6、PG7、PF8、PF9



# 原因

- Vbat会对PF6-PF11引脚有影响
  - en-us--TRM_M460_Series_EN_Rev1.03.PDF

![Figure_6.2-7](https://github.com/rickliu23/picture_resource/blob/main/recording-document/about_MCU/Nuvoton/RTC_influence_GPIO/Figure_6.2-7.png?raw=true)

![backup_domain](https://github.com/rickliu23/picture_resource/blob/main/recording-document/about_MCU/Nuvoton/RTC_influence_GPIO/backup_domain.png?raw=true)

+ 下图为RTC寄存器的某一个位说明，该位影响到了相关引脚的控制权

![bit_desp](https://github.com/rickliu23/picture_resource/blob/main/recording-document/about_MCU/Nuvoton/RTC_influence_GPIO/bit_desp.png?raw=true)



# 结论

- 装电池的情况下，3.3V断电后，系统会进入power-down模式
- 进入该模式时，RTC寄存器中的有一个位会自动置1
  - 置1时，部分引脚的控制权在RTC外设
  - 置0时，部分引脚的控制权在GPIO外设
- 3.3V电压上电时把这个位，将该位置0即可
