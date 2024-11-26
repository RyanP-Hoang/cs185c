# Issue Summary
The model had crashed due to a mismatch of what was stated in SIZE.h (1) and the actual number of logical processors (4). The current SIZE.h file is meant to be used with only one processor, not four.

# MITgcm Message
(PID.TID 0000.0001) *** ERROR *** EEBOOT_MINIMAL: No. of procs=    4 not equal to nPx*nPy=     1

(PID.TID 0000.0001) *** ERROR *** EEDIE: earlier error in multi-proc/thread setting

(PID.TID 0000.0001) *** ERROR *** PROGRAM MAIN: ends with fatal Error

# Issue Remedy
Fixed Size.h to match the actual number of CPU logical processors, increasing from 1 to 4.
