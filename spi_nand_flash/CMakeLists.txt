set(srcs "src/nand.c"
         "src/nand_winbond.c"
         "src/nand_gigadevice.c"
         "src/nand_alliance.c"
         "src/nand_micron.c"
         "src/nand_impl.c"
         "src/nand_impl_wrap.c"
         "src/nand_diag_api.c"
         "src/spi_nand_oper.c"
         "src/dhara_glue.c"
         "vfs/vfs_fat_spinandflash.c"
         "diskio/diskio_nand.c")

set(reqs fatfs)

if("${IDF_VERSION_MAJOR}.${IDF_VERSION_MINOR}" VERSION_GREATER "5.3")
    list(APPEND reqs esp_driver_spi)
else()
    list(APPEND reqs driver)
endif()

set(priv_reqs vfs)

idf_component_register(SRCS ${srcs}
        INCLUDE_DIRS include vfs diskio
        PRIV_INCLUDE_DIRS "priv_include"
        REQUIRES ${reqs}
        PRIV_REQUIRES ${priv_reqs})
