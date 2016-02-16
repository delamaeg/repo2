#*******************************************************************************
# System        : Europcar Greenway Project
# Subsystem     : Greenway Start/Stop Tools
# Module        : GWY_services_start
# $Source:  $
# Author(s)     : GEY Olivier
# Date          : 99/10/21
# $Revision: $
# Purpose       : Start Greenway Servives : submit, CCA, GWYC0141, etc
#
#******************************************************************************
*
NB_ERROR=0
check_return_code()
{
  [ "$?" -ne "0" ] && NB_ERROR=$(expr ${NB_ERROR} + 1)
} 

# --- Verifications prealables
if [ "0" -ne "$(id -u)" ]
then
	echo " ERROR $0 : You should be root to run this shell \n"
	exit 1
fi

if [[  "$#" -eq "0" || "$#" -eq "1" ]]
then
	NAME_GWY_ENV=$1
	echo " $0 : Greenway Services Startup For env :$NAME_GWY_ENV "
else
	echo " ERROR $0 : Bad Usage \n"
	echo " Usage : $0 [ENV_NAME] \n"
	exit 1
fi