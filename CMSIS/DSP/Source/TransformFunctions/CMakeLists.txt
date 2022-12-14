# Copyright (c) 2021 Stephanos Ioannidis <root@stephanos.io>
# SPDX-License-Identifier: Apache-2.0

zephyr_library()

zephyr_library_sources(
  arm_bitreversal.c
  arm_bitreversal2.c
  # NOTE: The ASM implementation of `arm_bitreversal2` is disabled for now in
  #       order to allow the compiler to perform ISA and microarchitecture-
  #       specific optimisations. This may be re-enabled in the future when we
  #       have a more advanced implementation that supports ARMv8.1-M MVE.
  # arm_bitreversal2.S
)

zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_FLOAT16
  arm_bitreversal_f16.c
  )

if(
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_16   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_32   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_64   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_128  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_256  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_512  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_1024 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_2048 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F64_4096
  )

  zephyr_library_sources(
    arm_cfft_f64.c
    arm_cfft_init_f64.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_16   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_32   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_64   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_128  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_256  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_512  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_1024 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_2048 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F32_4096
  )

  zephyr_library_sources(
    arm_cfft_radix2_f32.c
    arm_cfft_radix4_f32.c
    arm_cfft_radix8_f32.c
    arm_cfft_f32.c
    arm_cfft_init_f32.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_16   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_32   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_64   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_128  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_256  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_512  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_1024 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_2048 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_F16_4096
  )

  zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_FLOAT16
    arm_cfft_radix2_f16.c
    arm_cfft_radix4_f16.c
    arm_cfft_f16.c
    arm_cfft_init_f16.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_16   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_32   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_64   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_128  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_256  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_512  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_1024 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_2048 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q31_4096
  )

  zephyr_library_sources(
    arm_cfft_radix2_q31.c
    arm_cfft_radix4_q31.c
    arm_cfft_q31.c
    arm_cfft_init_q31.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_16   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_32   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_64   OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_128  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_256  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_512  OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_1024 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_2048 OR
  CONFIG_CMSIS_DSP_TABLES_CFFT_Q15_4096
  )

  zephyr_library_sources(
    arm_cfft_radix2_q15.c
    arm_cfft_radix4_q15.c
    arm_cfft_q15.c
    arm_cfft_init_q15.c
    )

endif()

zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_TABLES_CFFT_RADIX4_Q31  arm_cfft_radix4_init_q31.c)
zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_TABLES_CFFT_RADIX4_Q15  arm_cfft_radix4_init_q15.c)
zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_TABLES_CFFT_RADIX2_Q31  arm_cfft_radix2_init_q31.c)
zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_TABLES_CFFT_RADIX2_Q15  arm_cfft_radix2_init_q15.c)

if(
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_32    OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_64    OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_128   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_256   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_512   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_1024  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_2048  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F64_4096
  )

  zephyr_library_sources(
    arm_rfft_fast_f64.c
    arm_rfft_fast_init_f64.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_32    OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_64    OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_128   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_256   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_512   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_1024  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_2048  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F32_4096
  )

  zephyr_library_sources(
    arm_rfft_fast_f32.c
    arm_rfft_fast_init_f32.c
    arm_cfft_f32.c
    arm_cfft_init_f32.c
    arm_cfft_radix8_f32.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_32    OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_64    OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_128   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_256   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_512   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_1024  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_2048  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_FAST_F16_4096
  )

  zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_FLOAT16
    arm_rfft_fast_f16.c
    arm_rfft_fast_init_f16.c
    arm_cfft_f16.c
    arm_cfft_init_f16.c
    arm_cfft_radix8_f16.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_RFFT_F32_128  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_F32_512  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_F32_2048 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_F32_8192
  )

  zephyr_library_sources(
    arm_rfft_init_f32.c
    arm_rfft_f32.c
    arm_cfft_radix4_init_f32.c
    arm_cfft_radix4_f32.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_RFFT_F16_128  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_F16_512  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_F16_2048 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_F16_8192
  )

  zephyr_library_sources_ifdef(CONFIG_CMSIS_DSP_FLOAT16
    arm_cfft_radix4_init_f16.c
    arm_cfft_radix4_f16.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_32   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_64   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_128  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_256  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_512  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_1024 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_2048 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_4096 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q31_8192
  )

  zephyr_library_sources(
    arm_rfft_init_q31.c
    arm_rfft_q31.c
    arm_cfft_q31.c
    arm_cfft_init_q31.c
    arm_cfft_radix4_q31.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_32   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_64   OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_128  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_256  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_512  OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_1024 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_2048 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_4096 OR
  CONFIG_CMSIS_DSP_TABLES_RFFT_Q15_8192
  )

  zephyr_library_sources(
    arm_rfft_init_q15.c
    arm_rfft_q15.c
    arm_cfft_q15.c
    arm_cfft_init_q15.c
    arm_cfft_radix4_q15.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_DCT4_F32_128  OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_F32_512  OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_F32_2048 OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_F32_8192
  )

  zephyr_library_sources(
    arm_dct4_f32.c
    arm_dct4_init_f32.c

    arm_rfft_init_f32.c
    arm_rfft_f32.c
    arm_cfft_radix4_init_f32.c
    arm_cfft_radix4_f32.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q31_128  OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q31_512  OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q31_2048 OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q31_8192
  )

  zephyr_library_sources(
    arm_dct4_q31.c
    arm_dct4_init_q31.c

    arm_rfft_init_q31.c
    arm_rfft_q31.c
    arm_cfft_q31.c
    arm_cfft_init_q31.c
    arm_cfft_radix4_init_q31.c
    arm_cfft_radix4_q31.c
    )

endif()

if(
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q15_128  OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q15_512  OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q15_2048 OR
  CONFIG_CMSIS_DSP_TABLES_DCT4_Q15_8192
  )

  zephyr_library_sources(
    arm_dct4_q15.c
    arm_dct4_init_q15.c

    arm_rfft_init_q15.c
    arm_rfft_q15.c
    arm_cfft_q15.c
    arm_cfft_init_q15.c
    arm_cfft_radix4_init_q15.c
    arm_cfft_radix4_q15.c
    )

endif()
