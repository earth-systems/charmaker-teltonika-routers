#!/bin/sh                                                                                                                                                                                                                                                                               
echo "Appending lines to the existing /etc/config/firewall file to allow Tailscale to connect"
# First we define the block of code for the firewall config we need to set.                                                           
CONFIG_BLOCK="                                                                                                                        
config zone                                                                                                                           
    option device 'tailscale+'                                                                                                        
    option name 'tailscale'                                                                                       
    option src 'wan'                                                                                              
    option input 'ACCEPT'                                                                                         
    option forward 'REJECT'                                                                                       
    option output 'REJECT'                                                                                                            
"                                                                                                                                     
                                                                                                                  
# File path                                                                                                       
FILE_PATH="/etc/config/firewall"                                                                                  
                                                                                                                                                   
# Check if the configuration block already exists in the file                                                     
existing_block="false"                                                                                                                             
while IFS= read -r line; do                                                                                                                        
    if [[ "$line" == "config zone" ]]; then                                                                                                        
        if IFS= read -r next_line && [[ "$next_line" == "    option device 'tailscale+'" ]]; then                                                  
            if IFS= read -r next_line && [[ "$next_line" == "    option name 'tailscale'" ]]; then                
                existing_block="true"                                                                             
                break                                                                                             
            fi                                                                                                    
        fi                                                                                                        
    fi                                                                                                            
done < "$FILE_PATH"                                                                                               
                                                                                                                                                   
if [ "$existing_block" == "true" ]; then                                                                                                           
    echo "Configuration block already exists in $FILE_PATH."                                                                                       
else
    # Append the configuration block to the file                                                                                                   
    echo "$CONFIG_BLOCK" >> "$FILE_PATH"                                                                                                           
    echo "Configuration block added to $FILE_PATH."                                                                                                
fi                                                                                                                
