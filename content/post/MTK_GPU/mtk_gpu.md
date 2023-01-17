---
title: "在 MediaTek 设备上控制 GPU 频率"
date: 2023-01-17T19:01:08+08:00
draft: false
slug: "Mtk_gpu"
tags: ["Developer","Hardware"]
categories: ["Technology"]
---
#### gpufreq（/proc/gpufreq）
> 所有文件/操作在 MediaTek Dimensity 1200 和 MediaTek Helio G90T 上测试过  

读取当前设备支持的 GPU 频率：文件路径： `/proc/gpufreq/gpufreq_opp_dump`  
这是 MediaTek Dimensity 1200 的`gpufreq_opp_dump`:  
```
[00] freq = 886000, vgpu = 70000, vsram = 75000, posdiv = 4, gpu_power = 3352, aging = 1875
[01] freq = 879000, vgpu = 68125, vsram = 75000, posdiv = 4, gpu_power = 3252, aging = 1875
[02] freq = 873000, vgpu = 66250, vsram = 75000, posdiv = 4, gpu_power = 3154, aging = 1875
[03] freq = 867000, vgpu = 65000, vsram = 75000, posdiv = 4, gpu_power = 3059, aging = 1875
[04] freq = 861000, vgpu = 63125, vsram = 75000, posdiv = 4, gpu_power = 2996, aging = 1875
[05] freq = 854000, vgpu = 61250, vsram = 75000, posdiv = 4, gpu_power = 2965, aging = 1875
[06] freq = 848000, vgpu = 59375, vsram = 75000, posdiv = 4, gpu_power = 2873, aging = 1875
[07] freq = 842000, vgpu = 57500, vsram = 75000, posdiv = 4, gpu_power = 2813, aging = 1875
[08] freq = 836000, vgpu = 55625, vsram = 75000, posdiv = 4, gpu_power = 2725, aging = 1875
[09] freq = 825000, vgpu = 55625, vsram = 75000, posdiv = 4, gpu_power = 2638, aging = 1875
[10] freq = 815000, vgpu = 55625, vsram = 75000, posdiv = 4, gpu_power = 2581, aging = 1875
[11] freq = 805000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 2498, aging = 1875
[12] freq = 795000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 2416, aging = 1875
[13] freq = 785000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 2336, aging = 1875
[14] freq = 775000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 2309, aging = 1875
[15] freq = 765000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 2232, aging = 1875
[16] freq = 755000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 2156, aging = 1875
[17] freq = 745000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 2082, aging = 1875
[18] freq = 735000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1985, aging = 1875
[19] freq = 725000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1961, aging = 1875
[20] freq = 715000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1892, aging = 1875
[21] freq = 705000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1824, aging = 1250
[22] freq = 695000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1758, aging = 1250
[23] freq = 685000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1735, aging = 1250
[24] freq = 675000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1671, aging = 1250
[25] freq = 654000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1566, aging = 1250
[26] freq = 634000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1485, aging = 1250
[27] freq = 614000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1407, aging = 1250
[28] freq = 593000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1345, aging = 1250
[29] freq = 573000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1271, aging = 1250
[30] freq = 553000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1200, aging = 1250
[31] freq = 532000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1131, aging = 1250
[32] freq = 512000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1074, aging = 625
[33] freq = 492000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 1009, aging = 625
[34] freq = 471000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 946, aging = 625
[35] freq = 451000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 868, aging = 625
[36] freq = 431000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 811, aging = 625
[37] freq = 410000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 777, aging = 625
[38] freq = 390000, vgpu = 55000, vsram = 75000, posdiv = 4, gpu_power = 722, aging = 625
[39] freq = 370000, vgpu = 55000, vsram = 75000, posdiv = 8, gpu_power = 654, aging = 625
[40] freq = 350000, vgpu = 55000, vsram = 75000, posdiv = 8, gpu_power = 604, aging = 625
```
固定当前设备的 GPU 频率：文件路径：`/proc/gpufreq/gpufreq_opp_freq`  
这是 MediaTek Dimensity 1200 的 `gpufreq_opp_freq`  
```
[GPU-DVFS] fixed OPP is enabled  
```
如需固定频率，例如固定在 350000khz(无需重启等操作):  
```
[GPU-DVFS] fixed OPP is enabled
[40] freq = 350000, vgpu = 55000, vsram = 75000
```

### gpufreqv2
> 已在 MediaTek Dimensity 8100 上测试过

获取当前设备支持的 GPU 频率 :  `proc/gpufreqv2/stack_working_opp_table`  
这是 MediaTek Dimensity 8100 的 `stack_working_opp_table`  
```
[00] freq: 852000, volt: 67500, vsram: 75000, posdiv: 2, vaging: 0, power: 1691
[01] freq: 845000, volt: 66875, vsram: 75000, posdiv: 2, vaging: 0, power: 1638
[02] freq: 837000, volt: 66875, vsram: 75000, posdiv: 2, vaging: 0, power: 1622
[03] freq: 830000, volt: 66250, vsram: 75000, posdiv: 2, vaging: 0, power: 1570
[04] freq: 822000, volt: 66250, vsram: 75000, posdiv: 2, vaging: 0, power: 1554
[05] freq: 815000, volt: 65625, vsram: 75000, posdiv: 2, vaging: 0, power: 1520
[06] freq: 807000, volt: 65625, vsram: 75000, posdiv: 2, vaging: 0, power: 1504
[07] freq: 800000, volt: 65000, vsram: 75000, posdiv: 2, vaging: 0, power: 1455
[08] freq: 773000, volt: 65000, vsram: 75000, posdiv: 2, vaging: 0, power: 1410
[09] freq: 747000, volt: 64375, vsram: 75000, posdiv: 2, vaging: 0, power: 1334
[10] freq: 721000, volt: 63750, vsram: 75000, posdiv: 2, vaging: 0, power: 1289
[11] freq: 695000, volt: 63125, vsram: 75000, posdiv: 2, vaging: 0, power: 1202
[12] freq: 668000, volt: 63125, vsram: 75000, posdiv: 2, vaging: 0, power: 1158
[13] freq: 642000, volt: 62500, vsram: 75000, posdiv: 2, vaging: 0, power: 1089
[14] freq: 616000, volt: 61875, vsram: 75000, posdiv: 2, vaging: 0, power: 1022
[15] freq: 590000, volt: 61250, vsram: 75000, posdiv: 2, vaging: 0, power: 958
[16] freq: 572000, volt: 61250, vsram: 75000, posdiv: 2, vaging: 0, power: 931
[17] freq: 555000, volt: 60625, vsram: 75000, posdiv: 2, vaging: 0, power: 883
[18] freq: 538000, volt: 60000, vsram: 75000, posdiv: 2, vaging: 0, power: 856
[19] freq: 521000, volt: 59375, vsram: 75000, posdiv: 2, vaging: 0, power: 810
[20] freq: 504000, volt: 58750, vsram: 75000, posdiv: 2, vaging: 0, power: 766
[21] freq: 487000, volt: 58125, vsram: 75000, posdiv: 2, vaging: 0, power: 723
[22] freq: 470000, volt: 57500, vsram: 75000, posdiv: 2, vaging: 0, power: 681
[23] freq: 453000, volt: 56875, vsram: 75000, posdiv: 2, vaging: 0, power: 641
[24] freq: 436000, volt: 56875, vsram: 75000, posdiv: 2, vaging: 0, power: 618
[25] freq: 419000, volt: 56250, vsram: 75000, posdiv: 2, vaging: 0, power: 595
[26] freq: 402000, volt: 55625, vsram: 75000, posdiv: 2, vaging: 0, power: 557
[27] freq: 385000, volt: 55000, vsram: 75000, posdiv: 2, vaging: 0, power: 521
[28] freq: 368000, volt: 54375, vsram: 75000, posdiv: 3, vaging: 0, power: 487
[29] freq: 351000, volt: 53750, vsram: 75000, posdiv: 3, vaging: 0, power: 453
[30] freq: 334000, volt: 53125, vsram: 75000, posdiv: 3, vaging: 0, power: 421
[31] freq: 317000, volt: 52500, vsram: 75000, posdiv: 3, vaging: 0, power: 401
[32] freq: 304000, volt: 52500, vsram: 75000, posdiv: 3, vaging: 0, power: 381
[33] freq: 292000, volt: 51875, vsram: 75000, posdiv: 3, vaging: 0, power: 362
[34] freq: 280000, volt: 51250, vsram: 75000, posdiv: 3, vaging: 0, power: 342
[35] freq: 268000, volt: 50625, vsram: 75000, posdiv: 3, vaging: 0, power: 315
[36] freq: 255000, volt: 50625, vsram: 75000, posdiv: 3, vaging: 0, power: 306
[37] freq: 243000, volt: 50000, vsram: 75000, posdiv: 3, vaging: 0, power: 280
[38] freq: 231000, volt: 49375, vsram: 75000, posdiv: 3, vaging: 0, power: 263
[39] freq: 219000, volt: 48750, vsram: 75000, posdiv: 3, vaging: 0, power: 246
```
控制当前设备 GPU 频率：`proc/gpufreqv2/fix_custom_freq_volt`  
这是 MediaTek Dimensity 8100 的 `fix_custom_freq_volt`  
```
[GPUFREQ-DEBUG] fixed freq and volt are disabled
```
例如固定在 231000khz   
```
[GPUFREQ-DEBUG] fix freq: 231000 and volt: 49375
```

