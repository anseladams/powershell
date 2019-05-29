# powershell
powershell scripts that work
##ADGroups + Name + GroupCategory + Members
$adgroups = Get-ADGroup -Filter "name -like '*ggilje*'" | sort name

$data = foreach ($adgroup in $adgroups) {
    $members = $adgroup | get-adgroupmember | sort name
    foreach ($member in $members) {
        [PSCustomObject]@{
            Group   = $adgroup.name
            Members = $member
        }
    }
}

$data | export-csv "$env:userprofiles\desktop\groupinfo.csv" -NoTypeInformation

##
$Groups = Get-ADGroup -Properties * -Filter * -SearchBase "OU=Groups,OU=GSA,DC=USER,DC=root,DC=acgov,DC=org" 
Foreach($G In $Groups)
{
    Write-Host $G.Name
    Write-Host "-------------"
    $G.Members } 
    
    ##get a SID
    C:\Windows\System32\wbem>wmic useraccount where name="XXXXX" get sid
