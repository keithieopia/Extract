#!/bin/bash
# Extract for common file formats


if [ -z "$1" ]; then
    # display usage if no parameters given
    echo "Usage: extract <path/file_name>.<zip|rar|bz2|gz|tar|tbz2|tgz|Z|7z|xz|ex|tar.bz2|tar.gz|tar.xz>"
    echo "       extract <path/file_name_1.ext> [path/file_name_2.ext] [path/file_name_3.ext]"
else
    for n in "$@"
    do
        if [ -f "$n" ] ; then
            case $(file -b --mime-type "$n") in
                application/x-bzip2|application/x-gzip|application/x-xz|application/x-tar) 
                    tar xvf "$n"       ;;
                application/x-lzma)      
                    unlzma ./"$n"      ;;
                application/x-rar)       
                    unrar x -ad ./"$n" ;;
                application/zip)       
                    unzip ./"$n"       ;;
                application/x-compress)         
                    uncompress ./"$n"  ;;
                application/x-7z-compressed|application/x-arj|application/vnd.ms-cab-compressed|application/vnd.debian.binary-package|application/x-iso9660-image|application/x-lzh-compressed|application/x-msi|application/x-rpm|application/x-xar)
                    7za x ./"$n"        ;;
                application/x-dosexec)       
                    cabextract ./"$n"  ;;
                application/x-cpio)      
                    cpio -id < ./"$n"  ;;
                application/octet-stream)
                    # Fallback on file extension 
                    name=$(basename -- "$n")
                    ext=${FILENAME##*.}

                    case "$ext" in
                        chm|dmg|wim) 7za x ./"$n" ;;
                        exe) cabextract ./"$n"   ;; # sometimes shows as octet-stream, otherwise is x-dosexec
                    esac
                    ;;
                *)
                    echo "extract: '$n' - unknown archive method"
                    exit 1
                    ;;
            esac
        else
            echo "'$n' - file does not exist"
            exit 1
        fi
    done
fi
