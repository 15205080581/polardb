# 开启GPU加速计算 {#concept_lkt_hkd_5gb .concept}

GPU由于其特殊的硬件架构，在处理计算密集型、易于并行的程序上较CPU有很大的优势。

## 加速原理 {#section_jsl_3kd_5gb .section}

数据库中GPU并行加速是指对象级的并行，将单个字段的对象转换为适合并行计算的模型，利用GPU超多核心的能力并行计算，其并行计算示意图如下。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/124754/156773676438836_zh-CN.png)

## 注意事项 {#section_nfy_1nd_5gb .section}

对于并发数较大的场景，单个GPU设备会存在资源受限的情况，所以建议在会话中关闭GPU加速计算功能。

## 使用方法 {#section_est_kkd_5gb .section}

Ganos是通过检测GPU设备自动开启GPU加速计算，在实现函数上没有额外的参数设置，加速计算做到用户透明无感知；同时Ganos提供会话级控制权限，由用户决定是否启用GPU加速计算。

1.  确认当前环境是否有GPU设备。
    1.  创建ganos\_raster扩展"create extension ganos\_raster cascade"；
    2.  执行sql语句"select st\_checkgpu\(\)"。

        -   当前环境检测到GPU设备，成功返回GPU设备信息。

            ``` {#codeblock_buq_pva_4ac}
            rasterdb=# select st_checkgpu();
                                st_checkgpu                                                                                       
            ------------------------------------------------------------------------------------------------------------------------------
             [GPU(0) prop]multiProcessorCount=20; sharedMemPerBlock=49152; totalGlobalMem=-608239616; maxThreadsPerBlock=1024; maxThreadsPerMultiProcessor=2048; cudaThreadGetLimit=1024 .
            (1 row)
            ```

        -   当前环境未检测到GPU设备，则返回错误信息。

            ``` {#codeblock_w0b_b0f_sfg}
            rasterdb=# select st_checkgpu();
                               st_checkgpu                                                                
            ------------------------------------------------------------------------------------------------------------------------------------------ 
            There is not gpu device on current enviroment, cuda_errorcode=35, errormsg=CUDA driver version is insufficient for CUDA runtime version.
            (1 row)
            ```

        **说明：** 只有带GPU设备的环境才能启用GPU加速计算。

2.  开启和关闭会话级GPU使用状态。
    -   如果是带有GPU设备的环境，Ganos默认开启GPU加速计算，如果此时想关闭GPU加速计算，直接使用原来的CPU计算模式，则在会话中进行如下操作：

        执行set ganos.raster.use\_cuda=off

        ``` {#codeblock_d4r_aoz_ug4}
        rasterdb=# set ganos.raster.use_cuda=off;
        SET
        rasterdb=# show ganos.raster.use_cuda;
         ganos.raster.use_cuda 
        -----------------------
         off
        (1 row)
        ```

    -   如果要重新开启GPU加速计算，执行set ganos.raster.use\_cuda=on

``` {#codeblock_v05_2ew_xp8}
rasterdb=# set ganos.raster.use_cuda=on;
SET
rasterdb=# show ganos.raster.use_cuda;
 ganos.raster.use_cuda 
-----------------------
 on
(1 row)
```

3.  Ganos中实现GPU加速计算的模块。

    **说明：** 目前GPU加速计算仅在Ganos的Raster模块中应用实现，后续会增加Trajectory、Geometry模块的应用实现。


