project(WTF)

set(CMAKE_CXX_STANDARD 17)

# shuts up a *ton* of repeated warnings
add_compile_options(
	-Wno-gcc-compat
	-Wno-implicit-int-float-conversion
)

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}

	${CMAKE_CURRENT_SOURCE_DIR}/wtf
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/cf
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/cocoa
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/dtoa
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/ios
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/mac
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/persistence
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/posix
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/text
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/text/cf
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/text/cocoa
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/text/icu
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/threads
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/unicode
	${CMAKE_CURRENT_SOURCE_DIR}/wtf/unicode/icu

	# technically, we don't need this
	# the SDK has symlinks for these already
	${CMAKE_CURRENT_SOURCE_DIR}/darling/include

	${CMAKE_CURRENT_BINARY_DIR}/wtf/mac
)

mig(wtf/mac/MachExceptions.defs)

file(MAKE_DIRECTORY "${CMAKE_BINARY_DIR}/${DARLING_SDK_RELATIVE_PATH}/usr/include/wtf/mac")
create_symlink(
	"${DARLING_ROOT_RELATIVE_TO_SDK}/../../../../src/external/WTF/wtf/mac/MachExceptions.h"
	"${CMAKE_BINARY_DIR}/${DARLING_SDK_RELATIVE_PATH}/usr/include/wtf/mac/MachExceptions.h"
)
create_symlink(
	"${DARLING_ROOT_RELATIVE_TO_SDK}/../../../../src/external/WTF/wtf/mac/MachExceptionsServer.h"
	"${CMAKE_BINARY_DIR}/${DARLING_SDK_RELATIVE_PATH}/usr/include/wtf/mac/MachExceptionsServer.h"
)

add_darling_static_library(WTF FAT SOURCES
	wtf/ASCIICType.cpp
	wtf/Assertions.cpp
	wtf/AutomaticThread.cpp
	wtf/Bag.cpp
	wtf/BitVector.cpp
	wtf/BlockObjCExceptions.mm
	wtf/ClockType.cpp
	wtf/CompilationThread.cpp
	wtf/ConcurrentBuffer.cpp
	wtf/ConcurrentPtrHashSet.cpp
	wtf/CountingLock.cpp
	wtf/CPUTime.cpp
	wtf/CrossThreadCopier.cpp
	wtf/CrossThreadTaskHandler.cpp
	wtf/CryptographicallyRandomNumber.cpp
	wtf/CryptographicUtilities.cpp
	wtf/CurrentTime.cpp
	wtf/DataLog.cpp
	wtf/DateMath.cpp
	wtf/DebugHeap.cpp
	wtf/dtoa.cpp
	wtf/FastBitVector.cpp
	wtf/FastMalloc.cpp
	wtf/FilePrintStream.cpp
	wtf/FileSystem.cpp
	wtf/FunctionDispatcher.cpp
	wtf/Gigacage.cpp
	wtf/GlobalVersion.cpp
	wtf/GregorianDateTime.cpp
	wtf/HashTable.cpp
	wtf/HexNumber.cpp
	wtf/JSONValues.cpp
	wtf/JSValueMalloc.cpp
	wtf/Language.cpp
	wtf/Lock.cpp
	wtf/LockedPrintStream.cpp
	wtf/Logger.cpp
	wtf/MainThread.cpp
	wtf/MediaTime.cpp
	wtf/MemoryPressureHandler.cpp
	wtf/MetaAllocator.cpp
	wtf/MonotonicTime.cpp
	wtf/NumberOfCores.cpp
	wtf/ObjectIdentifier.cpp
	wtf/OSLogPrintStream.cpp
	wtf/OSRandomSource.cpp
	wtf/PageBlock.cpp
	wtf/ParallelHelperPool.cpp
	wtf/ParallelJobsGeneric.cpp
	wtf/ParkingLot.cpp
	wtf/PlatformRegisters.cpp
	wtf/PrintStream.cpp
	wtf/ProcessPrivilege.cpp
	wtf/PtrTag.cpp
	wtf/RAMSize.cpp
	wtf/RandomDevice.cpp
	wtf/RandomNumber.cpp
	wtf/ReadWriteLock.cpp
	wtf/RefCounted.cpp
	wtf/RefCountedArray.cpp
	wtf/RefCountedLeakCounter.cpp
	wtf/RunLoop.cpp
	wtf/Seconds.cpp
	wtf/SegmentedVector.cpp
	wtf/SHA1.cpp
	wtf/SixCharacterHash.cpp
	wtf/SizeLimits.cpp
	wtf/SmallPtrSet.cpp
	wtf/StackBounds.cpp
	wtf/StackPointer.cpp
	wtf/StackStats.cpp
	wtf/StackTrace.cpp
	wtf/StdFilesystem.cpp
	wtf/StringPrintStream.cpp
	wtf/ThreadGroup.cpp
	wtf/Threading.cpp
	wtf/ThreadMessage.cpp
	wtf/TimeWithDynamicClockType.cpp
	wtf/TimingScope.cpp
	wtf/TranslatedProcess.cpp
	wtf/UniqueArray.cpp
	wtf/URL.cpp
	wtf/URLHelpers.cpp
	wtf/URLParser.cpp
	wtf/UUID.cpp
	wtf/Vector.cpp
	wtf/WallTime.cpp
	wtf/WordLock.cpp
	wtf/WorkerPool.cpp
	wtf/WorkQueue.cpp
	wtf/WTFAssertions.cpp
	wtf/WTFConfig.cpp

	wtf/cf/CFURLExtras.cpp
	wtf/cf/FileSystemCF.cpp
	wtf/cf/LanguageCF.cpp
	wtf/cf/RunLoopCF.cpp
	wtf/cf/SchedulePairCF.cpp
	wtf/cf/URLCF.cpp

	wtf/cocoa/AutodrainedPool.cpp
	wtf/cocoa/CPUTimeCocoa.cpp
	wtf/cocoa/CrashReporter.cpp
	wtf/cocoa/Entitlements.mm
	wtf/cocoa/FileSystemCocoa.mm
	wtf/cocoa/LanguageCocoa.mm
	wtf/cocoa/MachSemaphore.cpp
	wtf/cocoa/MachSendRight.cpp
	wtf/cocoa/MainThreadCocoa.mm
	wtf/cocoa/MemoryFootprintCocoa.cpp
	wtf/cocoa/MemoryPressureHandlerCocoa.mm
	wtf/cocoa/NSURLExtras.mm
	wtf/cocoa/ResourceUsageCocoa.cpp
	wtf/cocoa/RuntimeApplicationChecksCocoa.cpp
	wtf/cocoa/SystemTracingCocoa.cpp
	wtf/cocoa/URLCocoa.mm
	wtf/cocoa/WorkQueueCocoa.cpp

	wtf/dtoa/bignum-dtoa.cc
	wtf/dtoa/bignum.cc
	wtf/dtoa/cached-powers.cc
	wtf/dtoa/diy-fp.cc
	wtf/dtoa/double-conversion.cc
	wtf/dtoa/fast-dtoa.cc
	wtf/dtoa/fixed-dtoa.cc
	wtf/dtoa/strtod.cc

	wtf/ios/WebCoreThread.cpp

	wtf/mac/FileSystemMac.mm
	wtf/mac/SchedulePairMac.mm

	${CMAKE_CURRENT_BINARY_DIR}/wtf/mac/MachExceptionsServer.c
	${CMAKE_CURRENT_BINARY_DIR}/wtf/mac/MachExceptionsUser.c

	wtf/persistence/PersistentCoders.cpp
	wtf/persistence/PersistentDecoder.cpp
	wtf/persistence/PersistentEncoder.cpp

	wtf/posix/FileSystemPOSIX.cpp
	wtf/posix/OSAllocatorPOSIX.cpp
	wtf/posix/ThreadingPOSIX.cpp

	wtf/text/ASCIILiteral.cpp
	wtf/text/AtomString.cpp
	wtf/text/AtomStringImpl.cpp
	wtf/text/AtomStringTable.cpp
	wtf/text/Base64.cpp
	wtf/text/CString.cpp
	wtf/text/ExternalStringImpl.cpp
	wtf/text/LineBreakIteratorPoolICU.cpp
	wtf/text/LineEnding.cpp
	wtf/text/StringBuffer.cpp
	wtf/text/StringBuilder.cpp
	wtf/text/StringBuilderJSON.cpp
	wtf/text/StringImpl.cpp
	wtf/text/StringView.cpp
	wtf/text/SymbolImpl.cpp
	wtf/text/SymbolRegistry.cpp
	wtf/text/TextBreakIterator.cpp
	wtf/text/TextStream.cpp
	wtf/text/WTFString.cpp

	wtf/text/cf/AtomStringImplCF.cpp
	wtf/text/cf/StringCF.cpp
	wtf/text/cf/StringImplCF.cpp
	wtf/text/cf/StringViewCF.cpp

	wtf/text/cocoa/StringCocoa.mm
	wtf/text/cocoa/StringImplCocoa.mm
	wtf/text/cocoa/StringViewCocoa.mm
	wtf/text/cocoa/TextBreakIteratorInternalICUCocoa.cpp
	wtf/text/cocoa/TextStreamCocoa.mm

	wtf/text/icu/UTextProvider.cpp
	wtf/text/icu/UTextProviderLatin1.cpp
	wtf/text/icu/UTextProviderUTF16.cpp

	wtf/threads/BinarySemaphore.cpp
	wtf/threads/Signals.cpp

	wtf/unicode/CollatorDefault.cpp
	wtf/unicode/UTF8Conversion.cpp

	wtf/unicode/icu/CollatorICU.cpp
	wtf/unicode/icu/ICUHelpers.cpp

	# benchmarks/ConditionSpeedTest.cpp
	# benchmarks/HashSetDFGReplay.cpp
	# benchmarks/LockFairnessTest.cpp
	# benchmarks/LockSpeedTest.cpp
	
	# wtf/generic/MainThreadGeneric.cpp
	# wtf/generic/MemoryFootprintGeneric.cpp
	# wtf/generic/MemoryPressureHandlerGeneric.cpp
	# wtf/generic/RunLoopGeneric.cpp
	# wtf/generic/WorkQueueGeneric.cpp

	# wtf/glib/ChassisType.cpp
	# wtf/glib/FileSystemGlib.cpp
	# wtf/glib/GLibUtilities.cpp
	# wtf/glib/GRefPtr.cpp
	# wtf/glib/GSocketMonitor.cpp
	# wtf/glib/RunLoopGLib.cpp
	# wtf/glib/SocketConnection.cpp
	# wtf/glib/URLGLib.cpp

	# wtf/linux/CurrentProcessMemoryStatus.cpp
	# wtf/linux/MemoryFootprintLinux.cpp

	# wtf/playstation/LanguagePlayStation.cpp
	# wtf/playstation/UniStdExtrasPlayStation.cpp

	# wtf/text/win/StringWin.cpp
	# wtf/text/win/TextBreakIteratorInternalICUWin.cpp

	# wtf/unix/CPUTimeUnix.cpp
	# wtf/unix/LanguageUnix.cpp
	# wtf/unix/MemoryPressureHandlerUnix.cpp
	# wtf/unix/UniStdExtrasUnix.cpp

	# wtf/win/CPUTimeWin.cpp
	# wtf/win/DbgHelperWin.cpp
	# wtf/win/FileSystemWin.cpp
	# wtf/win/LanguageWin.cpp
	# wtf/win/MainThreadWin.cpp
	# wtf/win/MemoryFootprintWin.cpp
	# wtf/win/MemoryPressureHandlerWin.cpp
	# wtf/win/OSAllocatorWin.cpp
	# wtf/win/PathWalker.cpp
	# wtf/win/RunLoopWin.cpp
	# wtf/win/ThreadingWin.cpp

	# wtf/fuchsia/CPUTimeFuchsia.cpp
	# wtf/text/unix/TextBreakIteratorInternalICUUnix.cpp
)
target_link_libraries(WTF bmalloc)
