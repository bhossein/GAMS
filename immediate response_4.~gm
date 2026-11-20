$TITLE Multiobjective Location-allocation Optimization with e-constraint method
$ontext
Explanation regarding the model will be inserted here
$offtext

$eolcom //
$STitle Model definitions

Sets
    k    objective functions / cost, time /
    m    main entery points    / mep1 /
    i    staging areas   / w1*w8 /
    p    points of demand in layer 1      / q1*q6 /
    j    points of demand in layer 2      / r1*r6 /
    h    points of demand in layer 3      / u1*u5 /
    t    time steps / t1*t35 /
*    d    districts  /d1*d7/
;
Parameter
   dir(k)  direction of the objective functions 1 for max and -1 for min
                               / cost -1, time -1 /;

Table tdm1(m,p) travel distance
               q1     q2      q3      q4      q5      q6
      mep1     130    90      75      80      150     80
;

Table tds1(i,p) travel distance
          q1        q2          q3         q4        q5         q6
    w1   100        120        180        230        320        230
    w2   210        190        160        90         80         80
    w3   150        130        90         90         120        110
    w4   100        115        145        200        130        80
    w5   90         70         80         140        210        54
    w6   100        80         45         120        200        330
    w7   140        90         60         185        220        274
    w8   260        225        210        90         15         200
;

Table tds2(i,j) travel distance
         r1         r2         r3         r4         r5         r6
    w1   160        200        200        275        250        350
    w2   115        225        190        25         70         105
    w3   235        175        130        60         52         140
    w4   180        160        160        240        215        390
    w5   86         60         95         170        145        250
    w6   130        120        32         160        130        240
    w7   150        145        50         180        152        260
    w8   280        275        235        60         120        35
*    w9   155        128        151        100        82         190        139
*    w10  73         51         114        65         163        272        220
*    w11  197        171        193        145        40         130        135
*    w12  271        244        268        218        127        74         27
*    w13  252        225        245        200        51         83         112
;

Table tdms(m,i) travel distance
           w1   w2   w3   w4   w5   w6   w7   w8
    mep1   200  90   32   160  90   75   100  135
;

Table ttm1(m,p) travel distance
               q1     q2      q3      q4      q5      q6
      mep1     250    210     190     230     360     190
;

Table tts1(i,p) travel distance
          q1        q2          q3         q4        q5         q6
    w1   200        210        295        500        350        200
    w2   400        350        360        200        630        430
    w3   300        270        260        200        180        250
    w4   215        225        290        380        270        180
    w5   140        120        150        300        570        350
    w6   190        200        70         270        470        310
    w7   300        190        100        450        500        380
    w8   520        500        500        260        40         290
;

Table tts2(i,j) travel time
         r1         r2         r3         r4         r5         r6
    w1   300        350        390        480        540        660
    w2   200        450        440        40         180        250
    w3   440        360        350        110        170        320
    w4   360        330        380        460        510        600
    w5   210        125        230        330        380        540
    w6   220        240        120        320        380        540
    w7   270        280        150        370        420        600
    w8   600        600        600        170        330        75
*    w9   275        255        350        230        155        310        212
*    w10  115        100        240        120        312        470        370
*    w11  352        333        420        290        77         255        202
*    w12  455        435        520        390        252        125        37
*    w13  445        426        510        390        102        190        213
;

Table ttms(m,i) travel time
           w1   w2   w3   w4   w5   w6   w7   w8
    mep1   350  180  80   320  190  180  200  320
;

Parameter

    recurring      rental + equipment + utilities + supplies + preprations  per month in dollars / 25000 /
    trktripcost    driving cost per km in dollars / 10 /
    heltripcost    tour cost of helicopter / 12000 /
    salary         HR slary per month in dollars / 17500 /
    dem1(p)        demand in first layer  /q1 147000, q2 260000, q3 246000, q4 211000, q5 125000, q6 405000/
    dem2(j)        demand in second layer / r1 89000, r2 74000, r3 56000, r4 32500, r5 47000, r6 50000 /
    dem3(h)        demand in third layer / u1 54000, u2 31000, u3 21500, u4 31000, u5 38000/
    max_msu        the maximum number of available MSUs  / 32 /
    trk_wcap       truck weight capacity in mTons / 15 /
    trc_wcap       tractor weight capacity in mTons / 3 /
*    tr_vcap  each truck volume capacity in m3 / 27.8 /
    hl_wcap        helicpter weight capacity in mTons / 2.5 /
    porkg          weight of each portion of relief package in kg / 5 /
    porvol         volume of each portion in m3 per kg  / 0.0015 /
    porsur         surface of each portion in m2 per kg  / 0.0004 /
    volcap         volume capacity of MSU in m3 0.8x320x3.75 / 960 /
    surcap         surface capacity of MSU in m2 0.8x320 / 256 /
    max_x          possible maximum number of x / 500000 /
;

Variables
*objectives
   z(k)
   cost                  objective function variables
   rcost                 total recurring cost
   trktrcost             total truck transportation cost
   hltrcost              total helicopter transportation cost
   hrcost                staff cost
*   satdem                satisfied demand
   time                 transportation time
*decision_variables
   xs1(t,i,p)           shipped item from SA to layer 1 in time t
   xs2(t,i,j)           shipped item from SA to layer 2 by truck
   xs2h(t,i,j)          shipped item from SA to layer 2 by helicopter
   xs3(t,i,h)           shipped item from SA to layer 3
   xm1(t,m,p)           shipped item from MEP to layer 1
   xms(t,m,i)           shipped item from MEP to SA in time t
   loc(i)               indicator for open location
   num_u(i)             number of MSUs in each location
   supplys1(i,p)        indicator for open shipment SA to layer 1
   supplys2(i,j)
   supplys2h(i,j)
   supplys3(i,h)
   supplym1(m,p)
   supplyms(m,i)         indicator for open shipment MEP to SA
   ldd(t)
*   l1dd(t)               indicator for day t in layer 1
*   l2dd(t)               indicator for day t in layer 2
*   l3dd(t)               indicator for day t in layer 3
   trktripms(m,i)        truck trips from MEP to SA
   trktripm1(m,p)        truck trips from MEP to layer 1
   trktrips1(i,p)        truck trips from SA to layer 1
   trktrips2(i,j)        tractor trips from SA to layer 2
   heltrips2(i,j)        helicopter trips from SA to layer 2
   heltrips3(i,h)        Helicopter trips from SA to layer 3
*   trnumi(m)             number of trucks departing from MEP
*quadartic)_terms
   quads1(t,i,p)         quadratic product of x and supply for layer 1
   quads2(t,i,j)
   quads2h(t,i,j)
   quads3(t,i,h)
   quadms(t,m,i)
   quadm1(t,m,p)
   quad_sec(i)           quadratic product of num_u and loc
Positive Variables  quads1, quads2, quads2h, quads3, quadms, quadm1, quad_sec
Integer Variables xs1, xs2, xs2h, xs3, xm1, xms, num_u, trktripms, trktripm1, trktrips1, trktrips2, heltrips2, heltrips3
Binary variables loc, ldd, supplys1, supplys2, supplys2h, supplys3, supplym1, supplyms;

Equations
    objcost              objective for minimizing cost in $
*   objcov    objective for maximizing satisfied demand in number
    objtime              objective for minimizing response time in days
    defrcost             definition recurring costs
    deftrktrcost         definition truck transportation costs
    defhltrcost          definition helicopter transportation costs
    defhrcost            definition HR costs
*    deftsd(j)            definition satisfied demand
*    deftcost             definition time cost
*    defx(j)              shipped items from SAs less than demands at associated POD
    defud1(p)            definition unsatisfied demand layer 1
    defud2(j)            definition unsatisfied demand layer 2
    defud3(h)            definition unsatisfied demand layer 3
    defxi(i)             balancing outgoing from SA with incoming from MEP
    one_1(p)
    one_2(j)
    one_3(h)             at least one SA per POD
    defdelta_s1(i,p)
    defdelta_m1(m,p)
    defdelta_s2(i,j)     eligible SA in terms of travel time
    defdelta_s2h(i,j)
    defnumu1(t,i)        required MSU with respect to volume
    defnumu2(t,i)        required MSU with respect to space
    defnumu3(i)          maximum number of msu that can be erected in each location
    defnumu4(i)
    defnumu5             MSU numbers constraint
    defnum5(t,m)
    defquads1_1(t,i,p)
    defquads1_2(t,i,p)
    defquads1_3(t,i,p)
    defquads2_1(t,i,j)
    defquads2_2(t,i,j)
    defquads2_3(t,i,j)
    defquads2h_1(t,i,j)
    defquads2h_2(t,i,j)
    defquads2h_3(t,i,j)
    defquads3_1(t,i,h)
    defquads3_2(t,i,h)
    defquads3_3(t,i,h)
    defquadm1_1(t,m,p)
    defquadm1_2(t,m,p)
    defquadm1_3(t,m,p)
    defquadms_1(t,m,i)
    defquadms_2(t,m,i)
    defquadms_3(t,m,i)
    defquadms_4(t,m)
    defquad_sec1(i)
    defquad_sec2(i)
    defquad_sec3(i)
    defl1dd(t,i)
    defl1dd_2(t,m)
    defl2dd(t,i)
    defl3dd(t)
    defl4dd(t)
    deftrnumcons(t,m)
    deftrktrips1(i,p)
    deftrktrips2(i,j)
    defheltrips2(i,j)
    deftrktripm1(m,p)
    deftrktripms(m,i)
    defheltrips3(i,h)
*    deftrnumi2(m)
*    deftrnumi3(m)
    defloc1(i,p)     SA open in i if some shipments are going to be from i to any j
    defloc2(i,j)
    defloc2h(i,j)
    defloc3(i,h)
    defloc4(i)
*    defsupplyi(i,j) oppened SA needs support from main entry point
*    cons1
*    cons2
*    cons3
*    cons4
*    cons5
;

*Objective functions
objcost..        z('cost') =e= rcost + trktrcost + hltrcost + hrcost;
objtime..        z('time') =e= sum(t,ldd(t))+ (2*sum(i,num_u(i)));
*objtime..        time =e= sum(t,ldd(t))+ (2*sum(i,num_u(i)));
defrcost..       rcost =e= sum(i, recurring * quad_sec(i));
deftrktrcost..   trktrcost =e= trktripcost * (sum((m,i), trktripms(m,i)*tdms(m,i))+sum((m,p),trktripm1(m,p)*tdm1(m,p))+sum((i,p),trktrips1(i,p)*tds1(i,p))+sum((i,j),trktrips2(i,j)*tds2(i,j)));
defhltrcost..    hltrcost =e=  heltripcost * (sum((i,j), heltrips2(i,j))+sum((i,h), heltrips3(i,h)));
defhrcost..      hrcost =e= sum(i,loc(i)*salary);
*deftotcost..    totcost =e= fcost + tcost + hrcost;
*objcov..        z('coverage') =e= satdem;
*deftsd..        satdem =e= sum((i,j),quad(i,j));
*defttime..       ttime =e= sum(t,l1dd(t)+l2dd(t)+l3dd(t)) - sum(t,l1dd(t)*l2dd(t)) - sum(t,l1dd(t)*l3dd(t)) - sum(t,l2dd(t)*l3dd(t)) + sum(t,l1dd(t)*l2dd(t)*l3dd(t));
*deftcost..       tcost =e= sum(t,ldd(t)) * 1000;

*Constraints
*defx(j)..                sum((i,t), x(i,j,t)) =l= d(j);
defud1(p)..              sum((t,i), quads1(t,i,p)) + sum((t,m), quadm1(t,m,p)) =g= dem1(p);
defud2(j)..              sum((t,i), quads2(t,i,j)) =g= dem2(j);
defud3(h)..              sum((t,i), quads3(t,i,h)) =g= dem3(h);
defxi(i)..               sum((t,p), quads1(t,i,p)) + sum((t,j), quads2(t,i,j)) +sum((t,j), quads2h(t,i,j)) + sum((t,h), quads3(t,i,h)) =l= sum((t,m), xms(t,m,i));
one_1(p)..               sum(i, supplys1(i,p)) + sum(m, supplym1(m,p)) =g= 1;
one_2(j)..               sum(i, supplys2(i,j)) + sum(i, supplys2h(i,j)) =g= 1;
one_3(h)..               sum(i, supplys3(i,h)) =g= 1;
defdelta_s1(i,p)..       supplys1(i,p)*tts1(i,p) =l= 400;
defdelta_m1(m,p)..       supplym1(m,p)*ttm1(m,p) =l= 400;
defdelta_s2(i,j)..       supplys2(i,j)*tts2(i,j) =l= 400;
defdelta_s2h(i,j)..      supplys2h(i,j)*tds2(i,j) =l= 200;
*deftsd(j)..              satdem (j) =e= sum(i,quad(i,j));
defnumu1(t,i)..          num_u(i) =g= (sum(p,xs1(t,i,p)) + sum(j, xs2(t,i,j))+ sum(j, xs2h(t,i,j))+ sum(h,xs3(t,i,h)))*porkg*porvol/volcap;
defnumu2(t,i)..          num_u(i) =g= (sum(p,xs1(t,i,p)) + sum(j, xs2(t,i,j))+ sum(j, xs2h(t,i,j))+ sum(h,xs3(t,i,h)))*porkg*porsur/surcap;
defnumu3(i)..            num_u(i) =l= 6*loc(i);
defnumu4(i)..            num_u(i) =g= loc(i);
defnumu5..               sum(i,num_u(i)) =l= max_msu;
defnum5(t,m)..           (sum((i), xms(t,m,i)) + sum((p), xm1(t,m,p)))* porkg * porsur =l= 2560;
defquads1_1(t,i,p)..     quads1(t,i,p) =l= supplys1(i,p)*max_x;
defquads1_2(t,i,p)..     quads1(t,i,p) =l= xs1(t,i,p);
defquads1_3(t,i,p)..     quads1(t,i,p) =g= xs1(t,i,p)-(max_x*(1-supplys1(i,p)));
defquads2_1(t,i,j)..     quads2(t,i,j) =l= supplys2(i,j)*max_x;
defquads2_2(t,i,j)..     quads2(t,i,j) =l= xs2(t,i,j);
defquads2_3(t,i,j)..     quads2(t,i,j) =g= xs2(t,i,j)-(max_x*(1-supplys2(i,j)));
defquads2h_1(t,i,j)..    quads2h(t,i,j) =l= supplys2h(i,j)*max_x;
defquads2h_2(t,i,j)..    quads2h(t,i,j) =l= xs2h(t,i,j);
defquads2h_3(t,i,j)..    quads2h(t,i,j) =g= xs2h(t,i,j)-(max_x*(1-supplys2h(i,j)));
defquads3_1(t,i,h)..     quads3(t,i,h) =l= supplys3(i,h)*max_x;
defquads3_2(t,i,h)..     quads3(t,i,h) =l= xs3(t,i,h);
defquads3_3(t,i,h)..     quads3(t,i,h) =g= xs3(t,i,h)-(max_x*(1-supplys3(i,h)));
defquadm1_1(t,m,p)..     quadm1(t,m,p) =l= supplym1(m,p)*max_x;
defquadm1_2(t,m,p)..     quadm1(t,m,p) =l= xm1(t,m,p);
defquadm1_3(t,m,p)..     quadm1(t,m,p) =g= xm1(t,m,p)-(max_x*(1-supplym1(m,p)));
defquadms_1(t,m,i)..     quadms(t,m,i) =l= supplyms(m,i)*max_x;
defquadms_2(t,m,i)..     quadms(t,m,i) =l= xms(t,m,i);
defquadms_3(t,m,i)..     quadms(t,m,i) =g= xms(t,m,i)-(max_x*(1-supplyms(m,i)));
defquadms_4(t,m)..       sum(i,xms(t,m,i))*porkg*porsur =l= 2560;
defquad_sec1(i)..        quad_sec(i) =l= loc(i)*max_msu;
defquad_sec2(i)..        quad_sec(i) =l= num_u(i);
defquad_sec3(i)..        quad_sec(i) =g= num_u(i)-(max_msu*(1-loc(i)));
defl1dd(t,i)..           ldd(t) * 25 =g= sum(p,quads1(t,i,p))* porkg/(1000 * trk_wcap);
defl1dd_2(t,m)..         ldd(t) * 25 =g= sum(p,quadm1(t,m,p))* porkg/(1000 * trk_wcap);
defl2dd(t,i)..           ldd(t) * 25 =g= sum(j,quads2(t,i,j))* porkg/(1000 * trc_wcap);
defl3dd(t)..             ldd(t) * 12 =g= (sum((i,j),quads2h(t,i,j))+ sum((i,h),quads3(t,i,h)))* porkg/(1000 * hl_wcap);
defl4dd(t)..             ldd(t) =l= sum((i,p),xs1(t,i,p))+sum((m,p),xm1(t,m,p))+sum((i,j),xs2(t,i,j))+sum((i,j),xs2h(t,i,j))+sum((i,h),xs3(t,i,h));
deftrnumcons(t,m)..      25 =g= sum(i,xms(t,m,i))* porkg/(1000 * trk_wcap);
deftrktrips1(i,p)..      trktrips1(i,p) =e= sum(t,quads1(t,i,p))* porkg/(1000 * trk_wcap);
deftrktrips2(i,j)..      trktrips2(i,j) =e= sum(t,quads2(t,i,j))* porkg/(1000 * trc_wcap);
defheltrips2(i,j)..      heltrips2(i,j) =e= sum(t,quads2h(t,i,j))* porkg/(1000 * hl_wcap);
deftrktripm1(m,p)..      trktripm1(m,p) =e= sum(t,quadm1(t,m,p))* porkg/(1000 * trk_wcap);
deftrktripms(m,i)..      trktripms(m,i) =e= sum(t,xms(t,m,i))* porkg/(1000 * trk_wcap);
defheltrips3(i,h)..      heltrips3(i,h) =e= sum(t,quads3(t,i,h))* porkg/(1000 * hl_wcap);
defloc1(i,p)..           loc(i) =g= supplys1(i,p);
defloc2(i,j)..           loc(i) =g= supplys2(i,j);
defloc2h(i,j)..          loc(i) =g= supplys2h(i,j);
defloc3(i,h)..           loc(i) =g= supplys3(i,h);
defloc4(i)..             loc(i) =l= sum(p,supplys1(i,p))+sum(j,supplys2(i,j))+sum(h,supplys3(i,h));
*defsupplyi(i,j)..        sum(m, supplyms(m,i)) =g= supply(i,j);
*cons1..            loc('w8')+loc('w10')=e=1;
*cons2..            loc('w4')+loc('w11')=e=1;
*cons3..            loc('w3')+loc('w13')=e=1;
*cons4..            loc('w13')+loc('w5')=e=1;
*cons5..            loc('w4')+loc('w9')=e=1;

xs1.up(t,i,p)=96000000;
xs2.up(t,i,j)=96000000;
xs2h.up(t,i,j)=96000000;
xs3.up(t,i,h)=96000000;
xm1.up(t,m,p)=96000000;
xms.up(t,m,i)=96000000;
*xi.up(m,i)=50000000;
*num_u.up(i)=320;
trktripms.up(m,i)=1000;
trktripm1.up(m,p)=1000;
trktrips1.up(i,p)=1000;
trktrips2.up(i,j)=1000;
*heltrips3.up(i,h)=1000;
Model example / all /;

$STitle eps-constraint method

Set k1(k)  the first element of k,
    km1(k) all but the first elements of k
    kk(k)  active objective function in constraint allobj;
k1(k)$(ord(k)=1) = yes; km1(k)=yes; km1(k1) = no;

Parameter
    rhs(k)     right hand side of the constrained obj functions in eps-constraint
    maxobj(k)  maximum value from the payoff table
    minobj(k)  minimum value from the payoff table
    numk(k)    ordinal value of k starting with 1
Scalar
    iter         total number of iterations
    infeas       total number of infeasibilities
    elapsed_time elapsed time for payoff and e-sonstraint
    start        start time
    finish       finish time
Variables
   a_objval   auxiliary variable for the objective function
   obj        auxiliary variable during the construction of the payoff table
   sl(k)      slack or surplus variables for the eps-constraints
Positive Variables sl
Equations
   con_obj(k) constrained objective functions
   augm_obj   augmented objective function to avoid weakly efficient solutions
   allobj     all the objective functions in one expression;

con_obj(km1)..   z(km1) - dir(km1)*sl(km1) =e= rhs(km1);

* We optimize the first objective function and put the others as constraints
* the second term is for avoiding weakly efficient points

augm_obj.. a_objval =e= sum(k1,dir(k1)*z(k1))
    + 1e-3*sum(km1,power(10,-(numk(km1)-1))*sl(km1)/(maxobj(km1)-minobj(km1)));

allobj..  sum(kk, dir(kk)*z(kk)) =e= obj;

Model mod_payoff    / example, allobj / ;
Model mod_epsmethod / example, con_obj, augm_obj / ;

Parameter
   payoff(k,k)  payoff tables entries;
Alias(k,kp);
*Alias(i,ip);

option optcr=0.02, limrow=0, limcol=0, solprint=off, solvelink=%Solvelink.LoadLibrary%;
*option limrow=0, limcol=0, solprint=off, solvelink=%Solvelink.LoadLibrary%;

* Generate payoff table applying lexicographic optimization
loop(kp,
  kk(kp)=yes;
  repeat
    solve mod_payoff using mip maximizing obj;
    if ( mod_payoff.modelstat = %ModelStat.Infeasible%
         or mod_payoff.modelstat = %ModelStat.Integer Infeasible%,
         Solve mod_payoff using RMIP maximizing obj);
    payoff(kp,kk) = z.l(kk);
    z.fx(kk) = z.l(kk); // freeze the value of the last objective optimized
    kk(k++1) = kk(k);   // cycle through the objective functions
  until kk(kp); kk(kp) = no;
* release the fixed values of the objective functions for the new iteration
  z.up(k) = inf; z.lo(k) =-inf;
);
if (mod_payoff.modelstat<>%ModelStat.Optimal% and
    mod_payoff.modelstat<>%ModelStat.Integer Solution%,
   abort 'no optimal solution for mod_payoff');

file fx  / results.txt /;
put fx ' PAYOFF TABLE'/   ;
loop (kp,
   loop(k, put payoff(kp,k):12:2);
   put /);

minobj(k)=smin(kp,payoff(kp,k));
maxobj(k)=smax(kp,payoff(kp,k));

* gridpoints are calculated as the range (difference between max and min) of
* the 2nd objective function from the payoff table
$if not set gridpoints $set gridpoints 20
Set g            grid points /g0*g%gridpoints%/
    grid(k,g)    grid
Parameter
    gridrhs(k,g) rhs of eps-constraint at grid point
    maxg(k)      maximum point in grid for objective
    posg(k)      grid position of objective
    firstOffMax, lastZero some counters
*    numk(k) ordinal value of k starting with 1
    numg(g)      ordinal value of g starting with 0
    step(k)      step of grid points in objective functions
*    loc(i)       locations
*    ow(i)       location
    jump(k)      jumps in the grid points traversing;

lastZero=1; loop(km1, numk(km1)=lastZero; lastZero=lastZero+1); numg(g) = ord(g)-1;

grid(km1,g) = yes; // Here we could define different grid intervals for different objectives
maxg(km1)   = smax(grid(km1,g), numg(g));
step(km1)   = (maxobj(km1)- minobj(km1))/maxg(km1);
gridrhs(grid(km1,g))$(dir(km1)=-1) = maxobj(km1) - numg(g)/maxg(km1)*(maxobj(km1)- minobj(km1));
gridrhs(grid(km1,g))$(dir(km1)= 1) = minobj(km1) + numg(g)/maxg(km1)*(maxobj(km1)- minobj(km1));

put / ' Grid points' /;
loop (g,
   loop(km1, put gridrhs(km1,g):12:2);
   put /);
put / 'Efficient solutions' /;

* Walk the grid points and take shortcuts if the model becomes infeasible or
* if the calculated slack variables are greater than the step size
posg(km1) = 0; iter=0; infeas=0; start=jnow;

repeat
  rhs(km1) = sum(grid(km1,g)$(numg(g)=posg(km1)), gridrhs(km1,g));
  solve mod_epsmethod maximizing a_objval using mip;
*  loop(ip, loc(i)=ow(i));
  iter=iter+1;
  if (mod_epsmethod.modelstat<>%ModelStat.Optimal% and
      mod_epsmethod.modelstat<>%ModelStat.Integer Solution%,
    infeas=infeas+1;   // not optimal is in this case infeasible
    put iter:5:0, '  infeasible' /;
    lastZero = 0; loop(km1$(posg(km1)>0 and lastZero=0), lastZero=numk(km1));
    posg(km1)$(numk(km1)<=lastZero) = maxg(km1); // skip all solves for more demanding values of rhs(km1)
  else
    put iter:5:0 ' ';
    loop(k, put z.l(k):15:0);
    loop(i, put loc.l(i):2:0);
    loop(i, put num_u.l(i):4:0);
*    loop(j, put ud.l(j):12:0);
*     loop(j, put satdem.l(j):12:0);
*     put ttime.l:12:0;
*    execute_unload 'trnsportdata.gdx', z,ow;
*    loop(ip$(loc(i)<>0), put i:12:2);
    jump(km1)=1;
*   find the first off max (obj function that hasn't reach the final grid point).
*   If this obj.fun is k then assign jump for the 1..k-th objective functions
*   The jump is calculated for the innermost objective function (km=1)
    jump(km1)$(numk(km1)=1)=1+floor(sl.L(km1)/step(km1));
    loop(km1$(jump(km1)>1), put '   jump');
    put /;
    );
* Proceed forward in the grid
  firstOffMax = 0;
  loop(km1$(posg(km1)<maxg(km1) and firstOffMax=0),
     posg(km1)=min((posg(km1)+jump(km1)),maxg(km1)); firstOffMax=numk(km1));
  posg(km1)$(numk(km1)<firstOffMax) = 0;
  abort$(iter>10000) 'more than 10000 iterations, something seems to go wrong'
until sum(km1$(posg(km1)=maxg(km1)),1)= card(km1) and firstOffMax=0;

finish=jnow; elapsed_time=(finish-start)*60*60*24;

put /;
*put / ' Locations' /;
*loop (i, put ow(i):12:2);
*put /;
put 'Infeasibilities = ', infeas:5:0 /;
put 'Elapsed time: ',elapsed_time:10:2, ' seconds' / ;
*execute 'gdxxrw.exe trnsportdata.gdx var=z.l(k) rng=sheet1!a1' ;
