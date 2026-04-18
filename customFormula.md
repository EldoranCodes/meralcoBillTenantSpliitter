formula to split the bills for all the tenants:

1. tenantNum is dyanmic. can be added and remove, no calcuation if 0 tenants.
2. getthe current usage per tenants. tenantConsumption = current - old submeter kwph recorded in the meter 
3. calculatedRateThisMonth =  MainBillingPrice(the price in the elec company or the main meters billing price) / MainMeterConsumption kwph
    total billing price and actual consumption is user input and will be found in  billing receipt provided
    example:
    total billing = 16431.76
    Main Meter recorded consumption = 1084
    apply the  formula 
    calculatedRateKwph: 15.1584 = 16431.76 / 1084
4. check if the number of tenants submeter over all consumption is equal to main meter consumption. it must tally. if not it will be deducted or added by tenant number in their sub meter consumption
  example:
  submeter consumption per tenant: tenant1 = 200, tenant2 =300, tenant3 = 250 tenant4 = 200
  total consumption of submeter: 200 + 300 +250 + 200 = 950 
  main meter consumption (provided) = 1106
  the difference will be added or dedcucted in submeters of the number of tenant
  1106-950 = 156 / 4 = 39
  39 is the difference if its posstive it will be deducted to the tenant per cosnume.
  tenant1 = 200 - 39 = 161
  tenant1 = 161 and so other tenants too.

  this case is when the main submeter is lessthan the total submeters.
    
  900-950 = -50 / 4 = 12.5
  12.5 is the difference  and it will be added to their per cosnume.
  tenant1 = 200 + 12.5 = 212.5
  tenant1 = 212.5 and so other tenants too.

now we have the calculatedRateThisMonth, consume per tenant
we can now calculate their respective price per consume
tenant1Bill = tenant1Consumed x calculatedRateThisMonth;
tenant2Bill = tenant1Consumed x calculatedRateThisMonth;
tenant3Bill = tenant1Consumed x calculatedRateThisMonth;
tenant4Bill = tenant1Consumed x calculatedRateThisMonth;

totalCalcualtedBillPertenant =  tenant1Bill + tenant2Bill + tenant3Bill + tenant4Bill;
and it must be equal to the MainBillingPrice

if totalCalcualtedBillPertenant == MainBillingPrice it means the formula is correct

then render the per tenants billing.


task:
1. input for MainBillingPrice, MainMeterConsumption that auto compute the calculatedRateThisMonth and rendered
2. dynamic addition of tenants from 1 to 10 tenants with auto display of tenant number, inputs of name, old consumption and the new consumption snapshot will be auto compute while inputting.
3. a button to calcualte the every tenants billing price for their consumption that wil lbe rendered via a table.



