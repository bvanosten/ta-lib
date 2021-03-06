#SET(TA_LIB_FLAGS "")
#SET(TA_LIB_INCLUDE_DIRS "")
#SET(TA_LIB_LIBRARY_DIRS "")
#SET(TA_LIB_LIBRARIES "")

SET(TA_LIB_VERSION_MAJOR 0)
SET(TA_LIB_VERSION_MINOR 6)
SET(TA_LIB_VERSION_BUILD 0)
SET(TA_LIB_VERSION_EXTRA "dev")

SET(TA_LIB_VERSION_FULL "${TA_LIB_VERSION_MAJOR}.${TA_LIB_VERSION_MINOR}.${TA_LIB_VERSION_BUILD}")
IF(TA_LIB_VERSION_EXTRA)
	SET(TA_LIB_VERSION_FULL "${TA_LIB_VERSION_FULL}-${TA_LIB_VERSION_EXTRA}")
ENDIF(TA_LIB_VERSION_EXTRA)

INCLUDE(CheckIncludeFiles)
INCLUDE(CheckFunctionExists)
INCLUDE(CheckTypeSize)
INCLUDE(CheckSymbolExists)
CHECK_INCLUDE_FILES(float.h HAVE_FLOAT_H)
CHECK_INCLUDE_FILES(inttypes.h HAVE_INTTYPES_H)
CHECK_INCLUDE_FILES(limits.h HAVE_LIMITS_H)
CHECK_INCLUDE_FILES(locale.h HAVE_LOCALE_H)
CHECK_INCLUDE_FILES(stddef.h HAVE_STDDEF_H)
CHECK_INCLUDE_FILES(stdint.h HAVE_STDINT_H)
CHECK_INCLUDE_FILES(stdlib.h HAVE_STDLIB_H)
CHECK_INCLUDE_FILES(string.h HAVE_STRING_H)
CHECK_INCLUDE_FILES(unistd.h HAVE_UNISTD_H)
CHECK_INCLUDE_FILES(wchar.h HAVE_WCHAR_H)
CHECK_INCLUDE_FILES(wctype.h HAVE_WCTYPE_H)
CHECK_FUNCTION_EXISTS(floor HAVE_FLOOR)
CHECK_FUNCTION_EXISTS(isascii HAVE_ISASCII)
CHECK_FUNCTION_EXISTS(localeconv HAVE_LOCALECONV)
CHECK_FUNCTION_EXISTS(mblen HAVE_MBLEN)
CHECK_FUNCTION_EXISTS(memmove HAVE_MEMMOVE)
CHECK_FUNCTION_EXISTS(memset HAVE_MEMSET)
CHECK_FUNCTION_EXISTS(modf HAVE_MODF)
CHECK_FUNCTION_EXISTS(pow HAVE_POW)
CHECK_FUNCTION_EXISTS(sqrt HAVE_SQRT)
CHECK_FUNCTION_EXISTS(strcasecmp HAVE_STRCASECMP)
CHECK_FUNCTION_EXISTS(strchr HAVE_STRCHR)
CHECK_FUNCTION_EXISTS(strerror HAVE_STRERROR)
CHECK_FUNCTION_EXISTS(strncasecmp HAVE_STRNCASECMP)
CHECK_FUNCTION_EXISTS(strrchr HAVE_STRRCHR)
CHECK_FUNCTION_EXISTS(strstr HAVE_STRSTR)
CHECK_FUNCTION_EXISTS(strtol HAVE_STRTOL)
CHECK_FUNCTION_EXISTS(strtoul HAVE_STRTOUL)
CHECK_FUNCTION_EXISTS(strcoll HAVE_STRCOLL)
CHECK_FUNCTION_EXISTS(strftime HAVE_STRFTIME)
CHECK_FUNCTION_EXISTS(vprintf HAVE_VPRINTF)
CHECK_TYPE_SIZE(ptrdiff_t SIZEOF_PTRDIFF_T)
IF(HAVE_SIZEOF_PTRDIFF_T)
	SET(HAVE_PTRDIFF_T 1)
ELSE()
	SET(HAVE_PTRDIFF_T 0)
ENDIF()
CHECK_TYPE_SIZE(size_t SIZEOF_SIZE_T)
IF(HAVE_SIZEOF_SIZE_T)
	SET(HAVE_SIZE_T 1)
ELSE()
	SET(HAVE_SIZE_T 0)
	SET(size_t "unsigned")
ENDIF()
CHECK_SYMBOL_EXISTS("struct tm" "sys/time.h" TM_IN_SYS_TIME)
CONFIGURE_FILE(include/ta_config.h.cmake include/ta_config.h)

SET(LIBRARY_OUTPUT_PATH ${ta-lib_BINARY_DIR}/lib/ CACHE PATH "Single out dir for all libs" FORCE)
SET(TA_LIB_LIBRARY_DIRS lib)
LINK_DIRECTORIES(${ta-lib_BINARY_DIR}/lib)

#SET(priv_HEADERS
#	src/ta_abstract/ta_frame_priv.h
#	src/ta_common/ta_global.h
#	src/ta_func/ta_utility.h
#	src/ta_abstract/ta_def_ui.h
#	src/ta_abstract/frames/ta_frame.h
#	src/ta_common/ta_magic_nb.h
#	src/ta_common/ta_memory.h
#)

SET(ta-lib_HEADERS
	include/ta_abstract.h
	include/ta_common.h
	include/ta_defs.h
	include/ta_func/c.h
	include/ta_libc.h
)

INCLUDE_DIRECTORIES(include
	src/ta_abstract 
	src/ta_abstract/frames
	src/ta_common
	src/ta_func
)

SET(ta-lib_CSOURCES
	src/ta_func/ta_LINEARREG.c
	src/ta_func/ta_MAX.c
	src/ta_func/ta_CDLHAMMER.c
	src/ta_func/ta_CDLDRAGONFLYDOJI.c
	src/ta_func/ta_CDLGRAVESTONEDOJI.c
	src/ta_func/ta_CDLABANDONEDBABY.c
	src/ta_func/ta_MAVP.c
	src/ta_func/ta_CDLCONCEALBABYSWALL.c
	src/ta_func/ta_HT_TRENDMODE.c
	src/ta_func/ta_IMI.c
	src/ta_func/ta_CDLADVANCEBLOCK.c
	src/ta_func/ta_AROONOSC.c
	src/ta_func/ta_CDLLONGLINE.c
	src/ta_func/ta_MIDPOINT.c
	src/ta_func/ta_PPO.c
	src/ta_func/ta_WMA.c
	src/ta_func/ta_HT_DCPHASE.c
	src/ta_func/ta_CDLSPINNINGTOP.c
	src/ta_func/ta_ACCBANDS.c
	src/ta_func/ta_CDLIDENTICAL3CROWS.c
	src/ta_func/ta_LINEARREG_ANGLE.c
	src/ta_func/ta_ADOSC.c
	src/ta_func/ta_CDL3OUTSIDE.c
	src/ta_func/ta_CORREL.c
	src/ta_func/ta_SMA.c
	src/ta_func/ta_ULTOSC.c
	src/ta_func/ta_AD.c
	src/ta_func/ta_CDLUPSIDEGAP2CROWS.c
	src/ta_func/ta_CDLUNIQUE3RIVER.c
	src/ta_func/ta_CDLRISEFALL3METHODS.c
	src/ta_func/ta_CDLLADDERBOTTOM.c
	src/ta_func/ta_PLUS_DM.c
	src/ta_func/ta_ADD.c
	src/ta_func/ta_STOCHRSI.c
	src/ta_func/ta_CDLHANGINGMAN.c
	src/ta_func/ta_NVI.c
	src/ta_func/ta_T3.c
	src/ta_func/ta_HT_PHASOR.c
	src/ta_func/ta_CDLTASUKIGAP.c
	src/ta_func/ta_DEMA.c
	src/ta_func/ta_RSI.c
	src/ta_func/ta_MIN.c
	src/ta_func/ta_CDLSTICKSANDWICH.c
	src/ta_func/ta_MINMAX.c
	src/ta_func/ta_CDLENGULFING.c
	src/ta_func/ta_CDLDOJI.c
	src/ta_func/ta_ACOS.c
	src/ta_func/ta_SAR.c
	src/ta_func/ta_CDLINNECK.c
	src/ta_func/ta_STOCH.c
	src/ta_func/ta_CDLPIERCING.c
	src/ta_func/ta_ASIN.c
	src/ta_func/ta_MACD.c
	src/ta_func/ta_KAMA.c
	src/ta_func/ta_ATR.c
	src/ta_func/ta_ADXR.c
	src/ta_func/ta_CDLCLOSINGMARUBOZU.c
	src/ta_func/ta_CDLDARKCLOUDCOVER.c
	src/ta_func/ta_TRIX.c
	src/ta_func/ta_HT_TRENDLINE.c
	src/ta_func/ta_ROCP.c
	src/ta_func/ta_CDLMORNINGSTAR.c
	src/ta_func/ta_MIDPRICE.c
	src/ta_func/ta_LOG10.c
	src/ta_func/ta_CDLGAPSIDESIDEWHITE.c
	src/ta_func/ta_SIN.c
	src/ta_func/ta_TSF.c
	src/ta_func/ta_STOCHF.c
	src/ta_func/ta_CMO.c
	src/ta_func/ta_CDL3STARSINSOUTH.c
	src/ta_func/ta_AROON.c
	src/ta_func/ta_TAN.c
	src/ta_func/ta_SINH.c
	src/ta_func/ta_utility.c
	src/ta_func/ta_TYPPRICE.c
	src/ta_func/ta_NATR.c
	src/ta_func/ta_CDL3BLACKCROWS.c
	src/ta_func/ta_HT_DCPERIOD.c
	src/ta_func/ta_CDLBREAKAWAY.c
	src/ta_func/ta_PLUS_DI.c
	src/ta_func/ta_STDDEV.c
	src/ta_func/ta_CDL2CROWS.c
	src/ta_func/ta_MOM.c
	src/ta_func/ta_TRIMA.c
	src/ta_func/ta_TRANGE.c
	src/ta_func/ta_CDLHIKKAKE.c
	src/ta_func/ta_CDLEVENINGDOJISTAR.c
	src/ta_func/ta_MAXINDEX.c
	src/ta_func/ta_FLOOR.c
	src/ta_func/ta_ROCR100.c
	src/ta_func/ta_CDLSEPARATINGLINES.c
	src/ta_func/ta_CDLHARAMICROSS.c
	src/ta_func/ta_WCLPRICE.c
	src/ta_func/ta_BBANDS.c
	src/ta_func/ta_CDLLONGLEGGEDDOJI.c
	src/ta_func/ta_CEIL.c
	src/ta_func/ta_AVGDEV.c
	src/ta_func/ta_MA.c
	src/ta_func/ta_CDLCOUNTERATTACK.c
	src/ta_func/ta_EXP.c
	src/ta_func/ta_CDLONNECK.c
	src/ta_func/ta_CDLINVERTEDHAMMER.c
	src/ta_func/ta_CDLXSIDEGAP3METHODS.c
	src/ta_func/ta_CDLMARUBOZU.c
	src/ta_func/ta_CCI.c
	src/ta_func/ta_MACDEXT.c
	src/ta_func/ta_CDLTHRUSTING.c
	src/ta_func/ta_CDLMATHOLD.c
	src/ta_func/ta_CDLHIKKAKEMOD.c
	src/ta_func/ta_CDLKICKINGBYLENGTH.c
	src/ta_func/ta_LINEARREG_INTERCEPT.c
	src/ta_func/ta_CDLKICKING.c
	src/ta_func/ta_SUB.c
	src/ta_func/ta_LINEARREG_SLOPE.c
	src/ta_func/ta_HT_SINE.c
	src/ta_func/ta_COSH.c
	src/ta_func/ta_CDLDOJISTAR.c
	src/ta_func/ta_CDLHOMINGPIGEON.c
	src/ta_func/ta_EMA.c
	src/ta_func/ta_COS.c
	src/ta_func/ta_SAREXT.c
	src/ta_func/ta_LN.c
	src/ta_func/ta_TANH.c
	src/ta_func/ta_MACDFIX.c
	src/ta_func/ta_OBV.c
	src/ta_func/ta_SUM.c
	src/ta_func/ta_DX.c
	src/ta_func/ta_TEMA.c
	src/ta_func/ta_MININDEX.c
	src/ta_func/ta_MULT.c
	src/ta_func/ta_APO.c
	src/ta_func/ta_DIV.c
	src/ta_func/ta_WILLR.c
	src/ta_func/ta_CDLSHORTLINE.c
	src/ta_func/ta_CDLRICKSHAWMAN.c
	src/ta_func/ta_MEDPRICE.c
	src/ta_func/ta_CDLMATCHINGLOW.c
	src/ta_func/ta_ROCR.c
	src/ta_func/ta_CDLBELTHOLD.c
	src/ta_func/ta_CDLTAKURI.c
	src/ta_func/ta_CDLTRISTAR.c
	src/ta_func/ta_CDLHARAMI.c
	src/ta_func/ta_PVI.c
	src/ta_func/ta_ATAN.c
	src/ta_func/ta_CDLHIGHWAVE.c
	src/ta_func/ta_CDLSTALLEDPATTERN.c
	src/ta_func/ta_VAR.c
	src/ta_func/ta_CDLEVENINGSTAR.c
	src/ta_func/ta_MAMA.c
	src/ta_func/ta_CDL3LINESTRIKE.c
	src/ta_func/ta_CDL3WHITESOLDIERS.c
	src/ta_func/ta_CDLSHOOTINGSTAR.c
	src/ta_func/ta_BOP.c
	src/ta_func/ta_MINUS_DM.c
	src/ta_func/ta_ROC.c
	src/ta_func/ta_CDLMORNINGDOJISTAR.c
	src/ta_func/ta_AVGPRICE.c
	src/ta_func/ta_MFI.c
	src/ta_func/ta_MINMAXINDEX.c
	src/ta_func/ta_MINUS_DI.c
	src/ta_func/ta_SQRT.c
	src/ta_func/ta_BETA.c
	src/ta_func/ta_CDL3INSIDE.c
	src/ta_func/ta_ADX.c
	src/ta_common/ta_version.c
	src/ta_common/ta_retcode.c
	src/ta_common/ta_global.c
	src/ta_abstract/frames/ta_frame.c
	src/ta_abstract/ta_abstract.c
	src/ta_abstract/ta_func_api.c
	src/ta_abstract/ta_def_ui.c
	src/ta_abstract/ta_group_idx.c
	src/ta_abstract/tables/table_t.c
	src/ta_abstract/tables/table_p.c
	src/ta_abstract/tables/table_a.c
	src/ta_abstract/tables/table_l.c
	src/ta_abstract/tables/table_r.c
	src/ta_abstract/tables/table_s.c
	src/ta_abstract/tables/table_c.c
	src/ta_abstract/tables/table_g.c
	src/ta_abstract/tables/table_f.c
	src/ta_abstract/tables/table_e.c
	src/ta_abstract/tables/table_o.c
	src/ta_abstract/tables/table_x.c
	src/ta_abstract/tables/table_q.c
	src/ta_abstract/tables/table_b.c
	src/ta_abstract/tables/table_n.c
	src/ta_abstract/tables/table_v.c
	src/ta_abstract/tables/table_y.c
	src/ta_abstract/tables/table_d.c
	src/ta_abstract/tables/table_i.c
	src/ta_abstract/tables/table_h.c
	src/ta_abstract/tables/table_z.c
	src/ta_abstract/tables/table_j.c
	src/ta_abstract/tables/table_k.c
	src/ta_abstract/tables/table_w.c
	src/ta_abstract/tables/table_u.c
	src/ta_abstract/tables/table_m.c
)

option(TA_STATIC_ONLY "Only build the static lib" OFF)

IF(TA_STATIC_ONLY)
	IF(UNIX)
		ADD_LIBRARY(ta_lib_static STATIC ${ta-lib_CSOURCES})
		SET_TARGET_PROPERTIES(ta_lib_static PROPERTIES OUTPUT_NAME ta_lib)
	ENDIF(UNIX)

	IF(WIN32)
		INCLUDE(GenerateExportHeader)
		ADD_LIBRARY(ta_lib_static STATIC ${ta-lib_CSOURCES})
		SET_TARGET_PROPERTIES(ta_lib_static PROPERTIES OUTPUT_NAME ta_lib_a)
	ENDIF(WIN32)

	SET_TARGET_PROPERTIES(ta_lib_static PROPERTIES SOVERSION ${TA_LIB_VERSION_FULL})

	INSTALL(FILES ${ta-lib_HEADERS} DESTINATION include/ta-lib)
	INSTALL(TARGETS ta_lib_static DESTINATION lib)
ELSE()
	IF(UNIX)
		ADD_LIBRARY(ta_lib SHARED ${ta-lib_CSOURCES})
		SET_TARGET_PROPERTIES(ta_lib PROPERTIES SOVERSION ${TA_LIB_VERSION_FULL} DEFINE_SYMBOL TA_LIB_SHARED)
		ADD_LIBRARY(ta_lib_static STATIC ${ta-lib_CSOURCES})
		SET_TARGET_PROPERTIES(ta_lib_static PROPERTIES OUTPUT_NAME ta_lib)
	ENDIF(UNIX)

	IF(WIN32)
		INCLUDE(GenerateExportHeader)
		ADD_LIBRARY(ta_lib SHARED ${ta-lib_CSOURCES})
		SET_TARGET_PROPERTIES(ta_lib PROPERTIES DEFINE_SYMBOL TA_LIB_SHARED)
		ADD_LIBRARY(ta_lib_static STATIC ${ta-lib_CSOURCES})
		SET_TARGET_PROPERTIES(ta_lib_static PROPERTIES OUTPUT_NAME ta_lib_a)
	ENDIF(WIN32)

	SET_TARGET_PROPERTIES(ta_lib PROPERTIES SOVERSION ${TA_LIB_VERSION_FULL})

	INSTALL(FILES ${ta-lib_HEADERS} DESTINATION include/ta-lib)
	INSTALL(TARGETS ta_lib ta_lib_static DESTINATION lib)
ENDIF(TA_STATIC_ONLY)

