## this project is to comptue the bill of 1 meter with 4 tennants deviding that one main meter bill

## we have 4 tennants

main meter
 - submeter1 (cel)
 -submeter2 (vic)
  -submter2.submeter1 (mhiles)
  -submter2.submeter2 (FREDA)

#input:
main meter consumptoin: xxxx kwh
main meter billing price: xxxxxx in peso

#computation: 

$RATE =  main meter price / main meter consumtion (kwh)

### compute the kwh consumed by tenants
cel consumption = new submter1.reading - old submter1.reading 

mhilesConsumption = new submter2.sumbter1.reading - old submter2.sumbter1.reading
``
fredaConsumtion = new submter2.sumbter2.reading - old submter2.sumbter2.reading

vic consumption = new submter2.reading - old submter2.reading - mhilesConsumption() - fredaConsumtion() 

### total all tenants consumption:

tenantsTotalConsumption = cel + mhiles + vic + freda;

diffOrOverKwh = main meter consumptoin - tenantsTotalConsumption;

if diff : diff/ 4 and add it to the tantns consumtion
if over: diff / 4 and reduce the tenatns consumption

then we will have new kwh per tenants

### computing the tenatns bill

newkwh per tennants * $RATE
