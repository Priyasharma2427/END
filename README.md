## Building Neural Network from Scratch.

#### 1 : We will create a neural network 

![image](https://user-images.githubusercontent.com/36500978/118193865-0b0d0a80-b466-11eb-829c-7754ba368c70.png)

In the given image, we are having:

- <b>Inputs</b> : i1, i2 
- <b>First hidden layer before activation</b> : h1,h2
- <b>First hidden layer after activation</b> : a_h1, a_h2
- <b>Output before activation function</b> : o1, o2
- <b>Output after activation</b> : a_o1, o_oh2
- <b>Weights</b> : w1, w2, w3, w4, w5, w6, w7, w8
- <b>Error from first input</b> : E1
- <b>Error from second input</b> : E2
- <b>Error</b> : E_total
- <b>Target</b> : we have two targets, t1 = 0.01 and t2 = 0.99. target is just the output which we are getting here i.e a_o1, a_o2

<b>Note: Do not have any biased
Activation layer is not just in hidden layer, it is in all the layers. </b>

Formulas : 
- h1 : w1*i1 + w2 *i2
- h2 : w3*i1 :w4*i2
- a_h1 : σ(h1)
- a_h2 : σ(h2)
- o1 : w5*a_h1 + w6*a_h2
- o2 : w7*a_h1 + w8*a_h2
- a_o1 : σ(o1)
- a_o2 : σ(o2)
- E1 = ½*(t1-a_o1)²
- E2 = ½*(t2-a_o2)²
- E_total = E1 + E2

#### 2 : Calculate all values and put them in the table.

![image](https://user-images.githubusercontent.com/36500978/118194045-56bfb400-b466-11eb-8494-00f0a2f35c10.png)



### Forward Propagation
<b> Values Given,</b> 
- inputs : i1 = 0.05, i2 = 0.1
- outputs : t1 = 0.01, t2 = 0.99
- Weights : w1 = 0.15, w2 = 0.2, w3 = 0.25, w4 = 0.3, w5 = 0.4, w6 = 0.45, w7 = 0.5, w8 = 0.55

<b>Values to be calculated,</b>
- We will be calculating these values using the above formulas in our excel sheet.
- h1, h2, a_h1, a_h2, o1, o2 , a_o1, a_o2 , E1, E2, E_total

<b> Till here, we were calulating forward propagation.Now we will be calculating backward propogation.</b>

### Backward propagation
To do backward propogation, we will start with <b>∂E_total/∂w5</b>.
In the above equation, we have removed E2 as it is not getting generated by w5. So we will not be using it. w5 is directly linked with E_total, but there are many steps in between. ∂(E1)/∂W5 has two things in between, i.e o1 and a_o1. We will be going through this route.

- <b> ∂E_total/∂w5  = ∂(E1 +E2)/∂W5 </b>
- <b> ∂E_total/∂w5  = ∂(E1)/∂W5 </b>

Chain rule, 

<b> ∂(E1)/∂W5 = ∂(E1)/∂(a_o1) * ∂(a_o1)/∂(o1) * ∂(o1)/∂w5 </b>

Now we will calculate the values of the above output.

<b> 1.</b>

 - ∂(E1)/∂(a_o1) =  ∂(½*(t1-a_o1)²) /  ∂(a_o1) 
 - ∂(E1)/∂(a_o1) =  (t1 – a_o1) * (-1)
 - <b> ∂(E1)/∂(a_o1) =   a_o1 - t1 </b>

<b> 2.</b>

 - ∂(a_o1)/∂(o1) =  ∂(σ(o1)) /  ∂(o1)
 - ∂(a_o1)/∂(o1) =  σ(o1) *  (1 -  σ(o1))
 - <b> ∂(a_o1)/∂(o1) =  a_o1 * (1 – a_o1) </b>

<b> 3.</b>

 - ∂(o1)/∂w5 = ∂(w5 * a_h1 + w6 * a_h2) / ∂w5 
 - <b> ∂(o1)/∂w5 = a_h1 </b>


Now,the equation will be :

- <b> ∂E_total / ∂w5 = (a_o1 – t1) * a_o1 * (1 – a_o1)) * a_h1 </b>

Similarly, we will find the equation for w6, w7, w8.

- <b> ∂E_total / ∂w6 = (a_o1 – t1) * a_o1 * (1 – a_o1)) * a_h2 </b>
- <b> ∂E_total / ∂w7 = (a_o2 – t2) * a_o2 * (1 – a_o2)) * a_h1 </b> 
- <b> ∂E_total / ∂w8 = (a_o2 – t2) * a_o2 * (1 – a_o2)) * a_h2 </b>

<b> Now, we will calculate values for w1, w2, w3, w4.   </b>

Before looking at w1, we will look at a_h1 value because w1 taking two routes i.e from a_o1 and a_o2
For that we will first calculate <b> ∂E_total/∂a_h1 </b> then will go to w1.

<b> ∂E_total / ∂a_h1 = ∂(E1 + E2) / ∂(a_h1) </b> 

This time we are having E1 as well as E2, as we have two routes.

   ∂(E1) / ∂(a_h1) = ∂E1/∂a_o1 * ∂a_o1/∂o1 * ∂o1/∂a_h1 
- <b> ∂(E1) / ∂(a_h1) = (a_o1 -t1) * (a_o1) * (1-a_o1) *w5 </b> 

     ∂(E2) / ∂(a_h1) = ∂E2/∂a_o2 * ∂a_o2/∂o2 * ∂o2/∂a_h1 
- <b>  ∂(E2) / ∂(a_h1) = (a_o2 -t2) * (a_o2) * (1-a_o2) *w7 </b> 

     ∂E_total / ∂a_h1 = ∂(E1 + E2) / ∂(a_h1) 
- <b>  ∂E_total / ∂a_h1 = (a_o1 -t1) * (a_o1) * (1-a_o1) *w5 + (a_o2 -t2) * (a_o2) * (1-a_o2) *w7 </b> 

Similary, we will calculate for ∂E_total / ∂a_h2

- <b>  ∂E_total / ∂a_h2 = (a_o2 -t2) * (a_o2) * (1-a_o2) *w8 + (a_o1 -t1) * (a_o1) * (1-a_o1) *w6 </b> 

Now we will calculate ∂E_total/∂w1 

- <b> ∂E_total/∂w1 = E_total/a_o1 * a_o1/o1 * o1/a_h1 * a_h1/h1 * h1/w1 </b> 
- <b> ∂E_total/∂w1 = ∂E_total/∂a_h1 * ∂a_h1/∂h1 * ∂h1/∂w1 </b> 
- <b> ∂E_total/∂w1 = ∂E_total/∂a_h1 * a_h1 * (1-a_h1) * ∂h1/∂w1 </b> 
- <b> ∂E_total/∂w1 = ∂E_total/∂a_h1 *a_h1 * (1- a_h1)*i1 </b> 

Similarly calculate for w2, w3 and w4,

- <b> ∂E_total/∂w2 = ∂E_total/∂a_h1 *a_h1 * (1- a_h1)*i2 </b> 
- <b> ∂E_total/∂w3 = ∂E_total/∂a_h2 *a_h2 * (1- a_h2)*i1 </b> 
- <b> ∂E_total/∂w4 = ∂E_total/∂a_h2 *a_h2 * (1- a_h2)*i2 </b> 

Now we are done with the calculation. Using these formulas we can find out the values of all the given variables.
Once done with the table, we can see in the error column that the error is decreasing. Now we will check with the different learning rates.

We will see how the learning rate is affecting the converging rate. if we have small learning rate, it will slow down the speed of training model, and i give it too high, it can cause undesirable divergent behavior to your loss function. That is why we need to find the optimal learning rate.

![image](https://user-images.githubusercontent.com/36500978/118196472-b4ee9600-b46a-11eb-8a4e-a81cd548b7bf.png)


![image](https://user-images.githubusercontent.com/36500978/118196484-ba4be080-b46a-11eb-8b9c-9b20be043932.png)


![image](https://user-images.githubusercontent.com/36500978/118196515-c3d54880-b46a-11eb-8342-3587d822e81b.png)


![image](https://user-images.githubusercontent.com/36500978/118196533-cfc10a80-b46a-11eb-815b-8905e2d81f4b.png)


![image](https://user-images.githubusercontent.com/36500978/118196573-df405380-b46a-11eb-94a0-5797b7b8c165.png)


![image](https://user-images.githubusercontent.com/36500978/118196665-0434c680-b46b-11eb-89dd-f2f62204b9cf.png)


This was all about Neural network from Scratch.
