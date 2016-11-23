configure_file(${CMAKE_CURRENT_SOURCE_DIR}/include/jasper/jas_config.h.in
  ${CMAKE_CURRENT_BINARY_DIR}/include/jasper/jas_config.h)

set(jasper_headers
  ${CMAKE_CURRENT_BINARY_DIR}/include/jasper/jas_config.h
  include/jasper/jasper.h
  include/jasper/jas_cm.h
  include/jasper/jas_fix.h
  include/jasper/jas_debug.h
  include/jasper/jas_getopt.h
  include/jasper/jas_icc.h
  include/jasper/jas_image.h
  include/jasper/jas_init.h
  include/jasper/jas_malloc.h
  include/jasper/jas_math.h
  include/jasper/jas_seq.h
  include/jasper/jas_stream.h
  include/jasper/jas_string.h
  include/jasper/jas_tmr.h
  include/jasper/jas_tvp.h
  include/jasper/jas_types.h
  include/jasper/jas_version.h)

set(jasper_base_sources
  base/jas_cm.c
  base/jas_debug.c
  base/jas_getopt.c 
  base/jas_image.c
  base/jas_icc.c
  base/jas_iccdata.c
  base/jas_init.c
  base/jas_malloc.c
  base/jas_seq.c
  base/jas_stream.c
  base/jas_string.c
  base/jas_tmr.c
  base/jas_tvp.c
  base/jas_version.c)

set(jasper_bmp_sources
  bmp/bmp_cod.h
  bmp/bmp_enc.h
  bmp/bmp_cod.c
  bmp/bmp_dec.c
  bmp/bmp_enc.c)

set(jasper_jp2_sources
  jp2/jp2_cod.h
  jp2/jp2_dec.h
  jp2/jp2_cod.c
  jp2/jp2_dec.c
  jp2/jp2_enc.c)

set(jasper_jpc_sources
  jpc/jpc_bs.h
  jpc/jpc_cod.h
  jpc/jpc_cs.h
  jpc/jpc_dec.h
  jpc/jpc_enc.h
  jpc/jpc_fix.h
  jpc/jpc_flt.h
  jpc/jpc_math.h
  jpc/jpc_mct.h
  jpc/jpc_mqcod.h
  jpc/jpc_mqdec.h
  jpc/jpc_mqenc.h
  jpc/jpc_qmfb.h
  jpc/jpc_tagtree.h
  jpc/jpc_t1cod.h
  jpc/jpc_t1dec.h
  jpc/jpc_t1enc.h
  jpc/jpc_tsfb.h
  jpc/jpc_t2cod.h
  jpc/jpc_t2dec.h
  jpc/jpc_t2enc.h
  jpc/jpc_util.h
  jpc/jpc_bs.c
  jpc/jpc_cs.c
  jpc/jpc_dec.c
  jpc/jpc_enc.c
  jpc/jpc_math.c
  jpc/jpc_mct.c
  jpc/jpc_mqcod.c
  jpc/jpc_mqdec.c
  jpc/jpc_mqenc.c
  jpc/jpc_qmfb.c
  jpc/jpc_tagtree.c
  jpc/jpc_t1cod.c
  jpc/jpc_t1dec.c
  jpc/jpc_t1enc.c
  jpc/jpc_tsfb.c
  jpc/jpc_t2cod.c
  jpc/jpc_t2dec.c
  jpc/jpc_t2enc.c
  jpc/jpc_util.c)

if (HAVE_LIBJPEG)
  set(jasper_jpg_misc_sources jpg/jpg_dec.c jpg/jpg_enc.c)
else()
  set(jasper_jpg_misc_sources jpg/jpg_dummy.c) 
endif()

set(jasper_jpg_sources
  ${jasper_jpg_misc_sources}
  jpg/jpg_cod.h
  jpg/jpg_enc.h
  jpg/jpg_jpeglib.h
  jpg/jpg_val.c)

set(jasper_mif_sources
  mif/mif_cod.h
  mif/mif_cod.c)

set(jasper_pgx_sources
  pgx/pgx_cod.h
  pgx/pgx_enc.h
  pgx/pgx_cod.c
  pgx/pgx_dec.c
  pgx/pgx_enc.c)

set(jasper_pnm_sources
  pnm/pnm_cod.h
  pnm/pnm_enc.h
  pnm/pnm_cod.c
  pnm/pnm_dec.c
  pnm/pnm_enc.c)

set(jasper_ras_sources
  ras/ras_cod.h
  ras/ras_enc.h
  ras/ras_cod.c
  ras/ras_dec.c
  ras/ras_enc.c)

add_library(libjasper
  ${jasper_headers}
  ${jasper_base_sources}
  ${jasper_bmp_sources}
  ${jasper_jp2_sources}
  ${jasper_jpc_sources}
  ${jasper_jpg_sources}
  ${jasper_mif_sources}
  ${jasper_pgx_sources}
  ${jasper_pnm_sources}
  ${jasper_ras_sources})

if (UNIX)
  set_target_properties(libjasper PROPERTIES LIBRARY_OUTPUT_NAME jasper)
endif()

target_include_directories(libjasper
  PUBLIC
  ${CMAKE_SOURCE_DIR}/src/libjasper/include
  ${CMAKE_BINARY_DIR}/src/libjasper/include)

install(FILES ${jasper_headers} DESTINATION include/jasper)
install(TARGETS libjasper
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib)
