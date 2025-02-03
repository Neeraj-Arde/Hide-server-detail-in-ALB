# Hide-server-detail-in-ALB
Server details are visible when we inspect the site.


login

$events = Get-WinEvent -FilterHashtable @{LogName = 'Security'; ID = 4624}
foreach ($event in $events) {
    $xml = [xml]$event.ToXml()
    $username = $xml.Event.EventData.Data | Where-Object {$_.Name -eq 'TargetUserName'} | Select-Object -ExpandProperty '#text'
    [pscustomobject]@{
        UserAccount = $username
        TimeCreated = $event.TimeCreated
    }
}


logout
$events = Get-WinEvent -FilterHashtable @{LogName = 'Security'; ID = 4634}
foreach ($event in $events) {
    $xml = [xml]$event.ToXml()
    $username = $xml.Event.EventData.Data | Where-Object {$_.Name -eq 'TargetUserName'} | Select-Object -ExpandProperty '#text'
    [pscustomobject]@{
        UserAccount = $username
        TimeCreated = $event.TimeCreated
    }
}
