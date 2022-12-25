```sh
://www.golinuxcloud.com/create-man-page-template-linux-with-examples/
.TH "SYSTEMSTATS" "8" "27 Oct 2020" "1.0" "SYSTEMSTATS man page"
.\" -------------------------------------------
.\" ------------------------------------------
.\" disable hyphenation
.nh
.\" disable justification (adjust text to left margin only)
.ad l
.\" ------------------------------------------
.\" * MAIN CONTENT STARTS HERE *
.\" ------------------------------------------
.SH "NAME"
systemStats \- retrieves information from host system
.SH "SYNOPSIS"
.HP \w'\fRsystemStats\fR\ 'u
\fRsystemStats\fR [\-t\ \fItemperature\fR] [\-f\ \fIfrequency\fR] [\-c\ \fIcores\fR] [\-V\ \fIVoltage\fR] [\-m\ \fIArmMemory\fR] [\-M\ \fIGPUMemory]\fR] [\-F\ \fIFreeMemory] [\-i\ \fIIPv4\fR] [\-v\ \fIVersionInfo\fR]
.br

.SH "DESCRIPTION"
.PP
\fRsystemStats\fR
Will gather the system core temperature, arm clock frequency, cores, voltage, arm/gpu memory, freememory and IP addresses.
.SH "OPTIONS"
.PP
\fB\-t\fR
.RS
   show temperature of core temp=##.##\&.
.RE
.PP
\fB\-f\fR
.RS
   show arm frequency in hertz\&.
.RE
.PP
\fR\-c\fR
.RS
   count the number of cores on device\&.
.RE
.PP
\fB\-V\fR
.RS
   get the current voltage of the system
.RE
.PP
\fB\-m\fR
.RS
   gets the current total memory allocated to the arm cpu
.RE
.PP
\fB\-M\fR
.RS
   gets the current total memory allocated to the GPU
.RE
.PP
\fB\-F\fR
.RS
   show arm frequency in hertz\&.
.RE
.PP
\fR\-c\fR
.RS
   count the number of cores on device\&.
.RE
.PP
\fB\-V\fR
.RS
   get the current voltage of the system
.RE
.PP
\fB\-m\fR
.RS
   gets the current total memory allocated to the arm cpu
.RE
.PP
\fB\-M\fR
.RS
   gets the current total memory allocated to the GPU
.RE
.PP
\fB\-F\fR
.RS
   gets the available free memory
.RE
.PP
\fB\-i\fR
.RS
   gets the IPv4 and IPv6 addresses
.RE
.PP
\fB\-v\fR
.RS
  return the version release date and author
.RE

.SH "NOTES"
This script will be developed over time to display more information using different options

.SH "BUGS"
Any bugs please forward them to the suggestion bin suggestion > /dev/null

.SH "AUTHORS"
Seb Blair <seb.blair@uog.ac.uk> <seb.blair@canterbury.ac.uk>
```