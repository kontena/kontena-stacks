# Kong Dashboard

Dashboard for managing [Kong](https://getkong.org/) gateway.

## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/quick-start).

Install Kong stack
`$ kontena stack install kontena/kong`

Install [Kong Dashboard](https://github.com/PGBI/kong-dashboard)
`$ kontena stack install kontena/kong-dashboard`

After it is deployed you can access the Dashboard with [Kontena VPN](http://kontena.io/docs/using-kontena/vpn-access.html):
- http://kong-dashboard.${GRID}.kontena.local:8080


**Note:** Replace `${GRID}` with your grid name.
