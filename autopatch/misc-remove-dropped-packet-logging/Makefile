NAME = $(shell basename $(shell pwd))
PATCH = misc/${NAME}.patch
TWEAKS =
TITLE = Remove Dropped Packet Logging
DESCRIPTION = Stop iptables from logging IPT_PACKET_DROPPED_NO_MATCH and needlessly clogging up /var/log/messages
CATEGORY = Misc
VERSIONS = 1.4.5-40 2.1.0-19 2.1.1-22 2.1.2-31 2.2.0-10 2.2.3-50 2.2.4-5 3.0.2-3 3.0.5-4
ICON = http://www.webos-internals.org/images/f/f9/Icon_WebOSInternals_Patch.png
SCREENSHOTS =
META_SUB_VERSION = 1

include ../common.mk

include ../modifications.mk

MAINTAINER = WebOS Internals
HOMEPAGE =