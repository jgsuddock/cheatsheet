# Getopts

## Arguments

```bash
# Positional Argument
POSITIONAL=$1
OPTIONAL_1=default_val
OPTIONAL_2=default_val
OPTIONAL_FLAG=0

# Usage info
show_help()
{
echo "
        Usage: Positional [-O Optional_1] [-F] [-P Optional_2]

        -O Optional_1   Optional field.
        -F              Flag field
        -P Optional_2   Optional field.

        For Example: ./script p1 -o opt1 -f -p opt2

        -H              Help
"
}
OPTIND=2
while getopts ":O:FP:" FLAG; do
  case "$FLAG" in
    O) # Set option "O" [Optional_1]
      OPTIONAL_1=$OPTARG
      ;;
    F) # Set option "F" [Flag]
      OPTIONAL_FLAG=1
      ;;
    P) # Set option "P" [Optional_2]
      OPTIONAL_2=$OPTARG
      ;;
    H) # help
      show_help
      ;;
    \?)
      echo "Invalid option: -$OPTARG. Use -H flag for help."
      exit 1
      ;;
  esac
done

echo "Positional=$POSITIONAL"
echo "Optional 1=$OPTIONAL_1"
echo "Optional 2=$OPTIONAL_2"
echo "Flag=$OPTIONAL_FLAG"
```

## Mixed Position and Optional Parameters

```bash
script_args=()
while [ $OPTIND -le "$#" ]
do
    if getopts h:f option
    then
        case $option
        in
            h) host="$OPTARG";;
            f) force=true;;
        esac
    else
        script_args+=("${!OPTIND}")
        ((OPTIND++))
    fi
done

echo "Host: $host\t\tForce: $force\t\t${script_args[@]}"
```

