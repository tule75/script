# script

### Add source docker to firewalld
`for net in $(docker network ls --format '{{.Name}}'); do
    subnet=$(docker network inspect $net -f '{{range .IPAM.Config}}{{.Subnet}}{{end}}')
    if [ -n "$subnet" ]; then
        sudo firewall-cmd --permanent --zone=trusted --add-source=$subnet
    fi
done
sudo firewall-cmd --reload`
