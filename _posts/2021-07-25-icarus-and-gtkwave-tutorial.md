---
layout: post
title: Icarus And GTKWave Tutorial
categories: Dev
tags: [beginner, verilog]
---

# 前言

有鑑於業界所使用的verilog IDE 功能太過繁複，因此紀錄Icarus、GTKWave的工具組合，方便進行小模組的功能驗證及測試。

<!-- more -->

# Installation

Linux(Debian/Ubuntu)

安裝Icarus

```bash
sudo apt-get install iverilog
```

安裝GTKWave

```bash
sudo apt-get install gtkwave
```

# Basic Parameter

| 參數   | 功能                           | 範例                                      |
| ------ | ------------------------------ | ----------------------------------------- |
| -o     | 和GCC的-o功能一樣，預設為a.out | iverilog -o test test.v                   |
| -y     | 指定調用模組的所在資料夾       | iverilog -y ./test/demo led_demo_tb.v     |
| -I     | 指定include的文件所在資料夾    | iverilog -I ./test/demo led_demo_tb.v     |
| -tvhdl | 將verilog檔案轉換至VHDL文件    | iverilog -tvhdl -o out_file.vhd in_file.v |

# Example

## module source code

```verilog
module led_demo(
    input clk,
    input rst_n,
    output reg led
);

reg [7:0] cnt;

always @ (posedge clk)
begin
    if(!rst_n)
        cnt <= 0;
    else if(cnt >= 10)
        cnt <= 0;
    else 
        cnt <= cnt + 1;
end

always @ (posedge clk)
begin
    if(!rst_n)
        led <= 0;
    else if(cnt == 10)
        led <= !led;
end

endmodule
```

## test bench

```verilog
`timescale 1ns/100ps

module led_demo_tb;

parameter SYSCLK_PERIOD = 10;

reg SYSCLK;
reg NSYSRESET;

initial
begin
    SYSCLK = 1'b0;
    NSYSRESET = 1'b0;
end

/*iverilog */
initial
begin            
    $dumpfile("wave.vcd");        
    $dumpvars(0, led_demo_tb);   
end
/*iverilog */

initial
begin
    #(SYSCLK_PERIOD * 10 )
        NSYSRESET = 1'b1;
    #1000
        $stop;
end

always @(SYSCLK)
    #(SYSCLK_PERIOD / 2.0) SYSCLK <= !SYSCLK;

led_demo led_demo_ut0 (
    // Inputs
    .rst_n(NSYSRESET),
    .clk(SYSCLK),

    // Outputs
    .led( led)
);

endmodule
```

**Nota Bene**:test bench內必須要有以下幾行，才可產生vcd文件。

```verilog
initial
begin            
    $dumpfile("wave.vcd");        
    $dumpvars(0, led_demo_tb);   
end
```

## compile

編譯source code

```bash
iverilog -o wave led_demo_tb.v led_demo.v
```

生成vcd文件

```bash
vvp -n wave -lxt2
```

開啟vcd文件

```bash
gtkwave wave.vcd
```

# Appendix

## compile VHDL source code

需要加入-g2012進行編譯

```bash
iverilog -g2012 led_demo.vhd
```

# Renference

[Icarus](http://iverilog.icarus.com/)
[GTKWave](http://gtkwave.sourceforge.net/)
[test source code](https://zhuanlan.zhihu.com/p/95081329)

