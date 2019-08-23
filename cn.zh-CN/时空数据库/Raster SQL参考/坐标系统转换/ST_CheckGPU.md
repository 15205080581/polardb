# ST\_CheckGPU {#reference_lfr_mhn_qfb19 .reference}

验证是否有GPU环境。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_r2w_s5d_r1z}
text  ST_CheckGPU();
```

## 描述 {#section_cxv_qhn_qfb .section}

验证当前数据库运行环境是否有可识别的GPU硬件设备。

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_ofo_zpx_rk8}
select st_checkgpu();

----------------------------------------------------------------------------------------
 [GPU prop]multiProcessorCount=20; sharedMemPerBlock=49152; maxThreadsPerBlock=1024

(1 row)
```

