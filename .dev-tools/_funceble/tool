#!/bin/bash

# _______           _        _______  _______  ______   _        _______
# (  ____ \|\     /|( (    /|(  ____ \(  ____ \(  ___ \ ( \      (  ____ \
# | (    \/| )   ( ||  \  ( || (    \/| (    \/| (   ) )| (      | (    \/
# | (__    | |   | ||   \ | || |      | (__    | (__/ / | |      | (__
# |  __)   | |   | || (\ \) || |      |  __)   |  __ (  | |      |  __)
# | (      | |   | || | \   || |      | (      | (  \ \ | |      | (
# | )      | (___) || )  \  || (____/\| (____/\| )___) )| (____/\| (____/\
# |/       (_______)|/    )_)(_______/(_______/|/ \___/ (_______/(_______/

# Written by: @Funilrys, Nissar Chababy <contact at funilrys dot com>

###############################  Text Format ###################################
# Red Color
red=$(tput setaf 1)

# White Color
white=$(tput setaf 7)

# Cyan Color
cyan=$(tput setaf 6)

# Magenta Color
magenta=$(tput setaf 5)

# Bold
bold=$(tput bold)

# Disable formating
normal=$(tput sgr0)
################################################################################
################################## Outputs #####################################
# We get the current dir we're working on
currentDir=${PWD}'/'

# Output of log
logOutput='output/logs/install.log'

# New output directory
outputDir="outputDir='${currentDir}output/'"

# Funilrys
funilrys="funilrys"
################################################################################
############################## Default Values ##################################
debug=false
# The file name of the script
script='funceble'

# Script online versionFile
onlineScript="https://raw.githubusercontent.com/${funilrys}/funceble/master/funceble"

# Quiet mode
quiet=false

# We get the content of the script
scriptContent=$(cat ${currentDir}${script} 2> ${logOutput})

# Default type
executionType='installation'

# Default seconds before timeout
secondsBeforeTimeout=30

# Version number
versionNumber='1.4.0'
################################################################################
# We log the date
date > ${logOutput}

################################# Delete/Uninstall #############################
# This part is the brain of the uninstallation logic
#
# @CalledBy Arguments Handle section
################################################################################
uninstall()
{
    # We ask for confirmation
    read -e -p "Do you really want to uninstall everything ? [Y/N] " uninstallConfirmation
    
    # We log and show message
    printf "Deletion of funceble" &&  printf "Deletion of funceble" >> ${logOutput}
    
    # We filter the confirmation
    case "${uninstallConfirmation}" in
        y|Y)
            # We delete everything
            cd "$(dirname $(echo ${currentDir}))"
            rm -fR ${currentDir} && printf "  ${cyan}✔${normal}\n\n"
            
            # We thank the user for using funceble
            printf "${bold}${green}Thank you for having used Funceble!!${normal}\n\n"
            printf "${bold}${green}You're not satisfied of Funceble?\nPlease let me know there: https://git.io/v7kAE ${normal}\n\n"
            exit 0
        ;;
        n|N|*)
            # We log and show on screen that we didn't delete anything
            printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
            printf "\n\n${bold}${green}Thank you for keeping funceble!!${normal}\n\n"
            exit 0
        ;;
    esac
}

################################## Usage #######################################
# Help function
#
# @CalledBy main, Arguments Handle Section
################################################################################
usage()
{
    echo "Usage: ${0} [ -d|--debug ] [ --help ] [ -t|--timeout ]"
    echo ""
    echo "       {[ -i|--installation ]} || {[ -p|--production ]} || {[ -u|--update ]}"
    echo "                                      {[ --del ]}"
    echo ""
    echo "  --debug                    -d              Activate the debug mode with the installation (${red}${bold}Must be before ${cyan}-u${normal} ${red}${bold}or ${cyan}-i${normal})"
    echo "  --del                                      Uninstall funceble and all its components"
    echo "  --help                                     Print this screen"
    echo "  --installation             -i              Execute the installation script"
    echo "  --production               -p              Prepare the repository for production"
    echo "  --timeout                  -t              Set the default timeout in seconds (${red}${bold}Must be before ${cyan}-u${normal} ${red}${bold}or ${cyan}-i${normal})"
    echo "  --update                   -u              Update the script"
    echo "  --version                  -v              Show the current version of Funceble"
    echo ""
}

################################## Script Exist ################################
# We check if the script exist
#
# @CalledBy installation
################################################################################
scriptExist()
{
    local fileToInstall="${1}"
    
    # We log && print message
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf 'Script exist' && printf 'Script exist' >> ${logOutput}
    fi
    if [[ -f "${fileToInstall}" ]]
    then
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${cyan}✔${normal}\n" && printf "  ✔\n" >> ${logOutput}
        fi
    else
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
            echo "The file ${fileToInstall} is not found"
        fi
        exit 0
    fi
}

############################### Script Readable ################################
# We check if the script is readable
#
# @CalledBy installation
################################################################################
scriptReadable()
{
    local fileToInstall="${1}"
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "Script readable" && printf "Script readable" >> ${logOutput}
    fi
    
    if [[ -r "${fileToInstall}" ]]
    then
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${cyan}✔${normal}\n" && printf "  ✔\n" >> ${logOutput}
        fi
    else
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
            echo "Impossible to read ${fileToInstall}" >> ${logOutput}
        fi
        exit 0
    fi
}

############################# Script Executable ################################
# We check if the script is executable
#
# @CalledBy installation
################################################################################
scriptExecutable()
{
    local fileToInstall="${1}"
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "Script executable" && printf "Script executable" >> ${logOutput}
    fi
    
    if [[ -x "${fileToInstall}" ]]
    then
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${cyan}✔${normal}\n" && printf "  ✔\n" >> ${logOutput}
        fi
    else
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
            echo "Please make sure that ${fileToInstall} is executable. You can execute 'chmod +x ${fileToInstall}' to make it executable" >> ${logOutput}
        fi
        exit 0
    fi
}

############################### Command Exist ##################################
# Check if a command exist
#
# @CalledBy awkInstalled, whoisInstalled, sedInstalled, sha512sumInstalled,
#           curlInstalled
################################################################################
commandexist()
{
    local commandToCheck="${1}"
    
    if hash ${commandToCheck} 2>/dev/null
    then
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${cyan}✔${normal}\n" && printf "  ✔\n" >> ${logOutput}
        fi
        
    else
        if [[ ${quiet} == false ]]
        then
            # We log && print message
            printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
            echo "Please make sure that ${red}${commandToCheck}${normal} is installed in your system."
        fi
        exit 0
    fi
}

############################# awk Installed ####################################
# We check if awk is installed
#
# @CalledBy installation
################################################################################
awkInstalled()
{
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "\n${bold}awk${normal} installed" && printf "awk installed" >> ${logOutput}
    fi
    
    commandexist 'awk'
}

############################## curl Installed ##################################
# We check if curl is installed
#
# @CalledBy installation
################################################################################
curlInstalled()
{
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "${bold}curl${normal} installed" && printf "curl installed" >> ${logOutput}
    fi
    
    commandexist 'curl'
}

############################## expect Installed ##################################
# We check if expect is installed
#
# @CalledBy installation
################################################################################
expectInstalled()
{
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "${bold}expect${normal} installed" && printf "expect installed" >> ${logOutput}
    fi
    
    commandexist 'expect'
}

############################### nslookup Installed ################################
# We check if nslookup is installed
#
# @CalledBy installation
################################################################################
nslookupInstalled()
{
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "${bold}nslookup${normal} installed" && printf "nslookup installed" >> ${logOutput}
    fi
    
    commandexist 'nslookup'
    
}

################################# sed Installed ################################
# We check if sed is installed
#
# @CalledBy installation
################################################################################
sedInstalled()
{
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "${bold}sed${normal} installed" && printf "sed installed" >> ${logOutput}
    fi
    
    commandexist 'sed'
}

############################## sha512sum Installed #############################
# We check if sha512sum is installed
#
# @CalledBy installation
################################################################################
sha512sumInstalled()
{
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "${bold}sha512sum${normal} installed" && printf "sha512sum installed" >> ${logOutput}
    fi
    
    commandexist 'sha512sum'
}

############################### whois Installed ################################
# We check if whois is installed
#
# @CalledBy installation
################################################################################
whoisInstalled()
{
    if [[ ${quiet} == false ]]
    then
        # We log && print message
        printf "${bold}whois${normal} installed" && printf "whois installed" >> ${logOutput}
    fi
    
    commandexist 'whois'
    
}

################################## Debug #######################################
# This part is the debug section
#
# @CalledBy scriptsWorkDir
################################################################################
debug()
{
    if [[ "${executionType}" == 'installation' ]]
    then
        if [[ ${debug} == true ]]
        then
            # Option if we want to debug
            regexDebug='debugUnknown=false'
            replaceBy="debugUnknown=true"
            sed -i "s|${regexDebug}|${replaceBy}|g" ${fileToInstall}
        fi
    elif [[ "${executionType}" == 'production' ]]
    then
        # Option if we want to debug
        regexDebug='debugUnknown=[a-z]*'
        replaceBy="debugUnknown=false"
        sed -i "s|${regexDebug}|${replaceBy}|g" ${fileToInstall}
    fi
}

################################## Text Format #################################
# Only for production.
# This part is used to fix changes to text format section
#
# @CalledBy scriptsWorkDir
################################################################################
textFormat()
{
    if [[ "${executionType}" == 'production' ]]
    then
        # We list the variable we have to change
        variableToCatch=('red=.*' 'white=.*' 'cyan=.*' 'magenta=.*' 'bold=.*' 'normal=.*')
        # We list the replacement we have to do
        changeWith=('red=$(tput setaf 1)' 'white=$(tput setaf 7)' 'cyan=$(tput setaf 6)' 'magenta=$(tput setaf 5)' 'bold=$(tput bold)' 'normal=$(tput sgr0)')
        
        for i in ${!variableToCatch[*]}
        do
            # We get the color
            regexColor="${variableToCatch[${i}]}"
            
            # We get the replacement
            replaceBy="${changeWith[${i}]}"
            
            # We apply changes
            sed -i "s|${regexColor}|${replaceBy}|g" ${fileToInstall}
        done
    fi
}

##################################### Status ###################################
# Only for production.
# This part is used to fix changes to status section
#
# @CalledBy scriptsWorkDir
################################################################################
status()
{
    if [[ "${executionType}" == 'production' ]]
    then
        # We list the variable we have to change
        variableToCatch=('validStatus=.*' 'invalidStatus=.*' 'errorStatus=.*' 'secondsBeforeTimeout=[0-9].*')
        # We list the replacement we have to do
        changeWith=('validStatus="ACTIVE"' 'invalidStatus="INVALID"' 'errorStatus="INACTIVE"' "secondsBeforeTimeout=${secondsBeforeTimeout}")
        
        for i in ${!variableToCatch[*]}
        do
            # We get the color
            regexStatus="${variableToCatch[${i}]}"
            
            # We get the replacement
            replaceBy="${changeWith[${i}]}"
            
            # We apply changes
            sed -i "s|${regexStatus}|${replaceBy}|g" ${fileToInstall}
        done
    fi
}

################################# Update IANA ##################################
# Update iana-domains-db
#
# @CalledBy installation
################################################################################
updateIANA()
{
    # We set the url where we get the needed informations
    local ianaURL="https://www.iana.org/domains/root/db"
    
    # Temporary file
    local curlIANA=/var/tmp/${funilrys}-iana
    
    # We delete old temporary files
    rm funilrys* &> /dev/null
    
    # We get a copy of the page
    curl -s ${ianaURL} -o ${curlIANA}
    
    while read -r line
    do
        # We get the valid domains extensions
        regex="(\/domains\/root\/db\/)(.*)(\.html)"
        
        if [[ "${line}" =~ ${regex} ]]
        then
            # We put it into a temporary file
            echo "${BASH_REMATCH[2]}" >> ${funilrys}_iana
        fi
    done < "${curlIANA}"
    
    # We move the generated file
    mv ${funilrys}_iana iana-domains-db
}

############################## Script Work Dir #################################
# We install the working directory into the script
#
# @CalledBy installation
################################################################################

scriptsWorkDir()
{
    if [[ ${quiet} == false ]]
    then
        if [[ "${executionType}" == 'installation' ]]
        then
            # We log && print message
            printf "\nInstallation of working directory" &&  printf "Installation of working directory" >> ${logOutput}
        elif [[ "${executionType}" == 'production' ]]
        then
            # We log && print message
            printf "\nDefault timeout: ${secondsBeforeTimeout} seconds" &&  printf "Default timeout: ${secondsBeforeTimeout} seconds" >> ${logOutput}
            printf "\nInstallation of default variables for production" &&  printf "Installation of default working directory for production" >> ${logOutput}
        fi
    fi
    
    regex="outputDir='.*\/output\/'"
    if [[ ${scriptContent} =~ ${regex} ]]
    then
        # We replace with the current working
        # directory an we print message
        if [[ "${executionType}" == 'production' ]]
        then
            outputDir="outputDir='%%currentDir%%/output/'"
        fi
        sed -i "s|${regex}|${outputDir}|g" ${fileToInstall}
        if [[ ${quiet} == false ]]
        then
            printf "  ${cyan}✔${normal}\n \n" && printf "  ✔\n" >> ${logOutput}
        fi
        
        # We run some important scripts
        debug
        textFormat
        status
        
        if [[ ${quiet} == false ]]
        then
            if [[ "${executionType}" == 'installation' ]]
            then
                echo "${bold}${cyan}The installation was successfully completed!${normal}"
                echo "You can now use the script with '${bold}./${script} [-OPTIONS]${normal}' or learn how to use it with '${green}${bold}./${script} --help${normal}'"
                printf '\n'
            elif [[ "${executionType}" == 'production' ]]
            then
                updateIANA
                echo "${bold}${cyan}The production logic was successfully completed!${normal}"
                echo "You can now distribute this repository."
                printf '\n'
            fi
        fi
        
    else
        if [[ ${quiet} == false ]]
        then
            if [[ "${executionType}" == 'installation' ]]
            then
                # We log && print message
                printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
                echo "Impossible to finalize installation."
            elif [[ "${executionType}" == 'production' ]]
            then
                printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
                echo "Impossible to finalize the poduction preparation."
            fi
        fi
        exit 0
    fi
}

############################### Installation ###################################
# This part is the brain of the installation system
#
# @CalledBy Arguments Handle section, update
################################################################################
installation()
{
    local fileToInstall="${1}"
    quiet=${2}
    
    # We check the script
    scriptExist "${fileToInstall}"
    scriptReadable "${fileToInstall}"
    scriptExecutable "${fileToInstall}"
    
    # We check dependencies
    awkInstalled
    curlInstalled
    expectInstalled
    nslookupInstalled
    sedInstalled
    sha512sumInstalled
    whoisInstalled
    
    # We finalize installation
    scriptsWorkDir
}

################################ checkVersion ##################################
# This part is where we check the version
#
# @CalledBy update
################################################################################
checkVersion()
{
    # We get the type
    type="${1}"
    
    if [[ "${type}" == 'get' ]]
    then
        # We download the script
        curl -s ${onlineScript} -o ${funilrys}
        # we give execution permission
        chmod +x ${funilrys}
        
        # We secretly execute a silent installation in the downloaded
        # script
        installation "${funilrys}" true
    fi
    
    # We get the sha512sum of the downloaded script
    local copiedVersion=$(sha512sum ${funilrys}|cut -d ' ' -f1)
    # We get the sha512sum of the already exist script
    local currentVersion=$(sha512sum ${currentDir}${script}|cut -d ' ' -f1)
    
    # We compare the versions
    if [[ ${currentVersion} == ${copiedVersion} ]]
    then
        # If the same == no need to update
        update=false
    else
        curlInstalled
        # If they are not the same == we need to update
        update=true
    fi
}

################################## Download Script #############################
# We download the script
#
# @CalledBy update
################################################################################
downloadScript()
{
    # We log && print message
    printf "\nDownload of the script" &&  printf "Download of the script" >> ${logOutput}
    
    # We check internet connection
    # If no internet connections are possible, we stop this script and
    # return a message error
    wget -q --tries=10 --timeout=20 --spider http://google.com
    
    if [[ $? != 0 ]]; then
        # We log && print message
        printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
        echo "Impossible to update ${currentDir}${script}. Please report issue." >> ${logOutput}
        exit 0
    else
        # We save the online script into the existing one
        curl -s ${onlineScript} -o "${currentDir}${script}"
        # We log && print message
        printf "  ${cyan}✔${normal}\n\n" && printf "  ✔\n" >> ${logOutput}
    fi
}

################################## Update ######################################
# This part is the brain of update
#
# @CalledBy Arguments Handle section
################################################################################
update()
{
    if [[ -d ${currentDir}.git ]]
    then
        git pull
    else
        # We get the online version and compare versions
        checkVersion 'get'
        
        if [[ ${update} == true ]]
        then
            # We only need to execute if the versions are not the same
            
            downloadScript
            
            # We install the new script
            installation ${currentDir}${script} true
            # We log && print message
            printf "Checking Version" &&  printf "Checking Version" >> ${logOutput}
            
            # We check the version of the newly downloaded script
            checkVersion
            
            if [[ ${update} == false ]]
            then
                # If we don't need to update, here's the end
                # We log && print message
                printf "  ${cyan}✔${normal}\n\n" && printf "  ✔\n" >> ${logOutput}
                echo "${bold}${cyan}The update was successfully completed!${normal}"
                printf '\n'
                
                # We delete the temporary file and stop the script
                rm -f "${funilrys}"
                exit 1
            else
                # We log && print message
                printf "  ${red}✘${normal}\n" && printf "  ✘\n" >> ${logOutput}
                echo "Impossible to update ${currentDir}${script}. Please report issue." >> ${logOutput}
                exit 0
            fi
        else
            # We log && print message
            printf "No need to update.\n" &&  printf "No need to update." >> ${logOutput}
            rm -f "${funilrys}"
            exit 1
        fi
    fi
}


############################### Arguments Handle ###############################
# We use this part to get arguments from command line.
#
# @Requiredby All
################################################################################
while [ "$#" -gt 0 ]; do
    case "$1" in
        # We catch if we have to activate debug on installation
        -d|--debug)
            debug=true
            shift 1
        ;;
        # We catch if we have to uninstall everything
        --del)
            uninstall
            shift 1
        ;;
        # We catch if we have to show usage()
        -h|--help)
            usage
            shift 1
        ;;
        # We catch if we have to install only the script
        -i|--install)
            installation "${currentDir}${script}" false
            shift 1
        ;;
        -p|--production)
            executionType='production'
            installation "${currentDir}${script}" false
            shift 1
        ;;
        # We catch the default timeout we have to set
        -t|--timeout)
            secondsBeforeTimeout="${2}"
            shift 2
        ;;
        # We catch if we have to update the script
        -u|--update)
            update
            shift 1
        ;;
        # We catch if we have to show the version number
        -v|--version)
            echo "Current Version: ${versionNumber}"
            exit 1
        ;;
        -*)
            echo "Unknown option: $1" >&2
            exit 1
        ;;
        *)
            usage
            shift 1
        ;;
    esac
done
