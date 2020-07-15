---
title: "How NOT to calculate gender gaps in wages"
published: true
---


# Gender Gaps In Earnings: How NOT To

A typical mistake in assessing gender gaps in earnings is trying to adjust it for endogenous variables, like job type and title. This mistake is commonly made in public debates, with various pundits claiming that the *actual* gender gap is much lower that what people report, because we need to compare men and women working in the same position.

This argument is persuasive at a superficial level: that in order to assess whether discrimination actually takes place in the labor market we should compare men and women *everything else equal* makes sense, intuitively. In reality, assessing the extent of discrimination and quantifying this effect is extremely challenging and complex. This small note does not aim at showing how we can detect discrimination in the labor market. I would refer to a course in advanced labor economics for that. More modestly, this note aims at using an elementary example to debunk this common mistake.

### Genesys: And Lo, Men and Women Were Created Equally

Let's take the extremely simple example of ten working men and ten working women, with the exact same characteristics. Each of the ten men has a level of ability or skill ranging from 1 to 10. Women are generated in exactly the same way. We are in other words in a situation of perfect equality in abilities and skills.


```python
# Simulate
import numpy as np
import pandas as pd

data = {
    'ability': list(range(1,11))*2,
    'gender': ['male']*10 + ['female']*10, 
}

data = pd.DataFrame(data)
data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ability</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>male</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>male</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>male</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>male</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>male</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>male</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>male</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>male</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>female</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>female</td>
    </tr>
    <tr>
      <th>12</th>
      <td>3</td>
      <td>female</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4</td>
      <td>female</td>
    </tr>
    <tr>
      <th>14</th>
      <td>5</td>
      <td>female</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6</td>
      <td>female</td>
    </tr>
    <tr>
      <th>16</th>
      <td>7</td>
      <td>female</td>
    </tr>
    <tr>
      <th>17</th>
      <td>8</td>
      <td>female</td>
    </tr>
    <tr>
      <th>18</th>
      <td>9</td>
      <td>female</td>
    </tr>
    <tr>
      <th>19</th>
      <td>10</td>
      <td>female</td>
    </tr>
  </tbody>
</table>
</div>



### The Fall From Eden: Promotions and Wages

At this stage, I decide to promote some of my workers to managerial positions. Obviously anyone with a skill level above 8 will be promoted, these are excellent people, whether they are men or women. However, I need more managers, and for whatever reason (they posture more, they ask for a promotion, they are my drinking buddies) I decide to fill up the remaining managerial positions only with the best of the remaining (mediocre) men. 

Then I set wages. As a baseline, I decide to give people a wage equal to twice their ability level if they are managers, and a wage equal their ability level if they are not managers. However, I am also discriminating in wages. So I cut the wage of each woman by 10%.

In other words, I am discriminating against women in two separate ways. First I do not promote them (ah, the glass ceiling!). Second, I pay them less.


```python
data.loc[:, 'manager'] = (data.loc[:, 'ability']>8) | ((data.loc[:, 'gender']=='male') & (data.loc[:, 'ability']>5))

data.loc[:, 'wages'] = data.loc[:, 'ability'] + data.loc[:, 'ability']*data.loc[:, 'manager']
data.loc[:, 'wages'] = data.loc[:, 'wages'] - 0.1*(data.loc[:, 'gender']=='female')*data.loc[:, 'wages']

data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ability</th>
      <th>gender</th>
      <th>manager</th>
      <th>wages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>male</td>
      <td>False</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>male</td>
      <td>False</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>male</td>
      <td>False</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>male</td>
      <td>False</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>male</td>
      <td>False</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>male</td>
      <td>True</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>male</td>
      <td>True</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>male</td>
      <td>True</td>
      <td>16.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>male</td>
      <td>True</td>
      <td>18.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>male</td>
      <td>True</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>female</td>
      <td>False</td>
      <td>0.9</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>female</td>
      <td>False</td>
      <td>1.8</td>
    </tr>
    <tr>
      <th>12</th>
      <td>3</td>
      <td>female</td>
      <td>False</td>
      <td>2.7</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4</td>
      <td>female</td>
      <td>False</td>
      <td>3.6</td>
    </tr>
    <tr>
      <th>14</th>
      <td>5</td>
      <td>female</td>
      <td>False</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6</td>
      <td>female</td>
      <td>False</td>
      <td>5.4</td>
    </tr>
    <tr>
      <th>16</th>
      <td>7</td>
      <td>female</td>
      <td>False</td>
      <td>6.3</td>
    </tr>
    <tr>
      <th>17</th>
      <td>8</td>
      <td>female</td>
      <td>False</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>18</th>
      <td>9</td>
      <td>female</td>
      <td>True</td>
      <td>16.2</td>
    </tr>
    <tr>
      <th>19</th>
      <td>10</td>
      <td>female</td>
      <td>True</td>
      <td>18.0</td>
    </tr>
  </tbody>
</table>
</div>



### Honest Gender Gaps

We all agree that there is a sizable amount of gender discrimination in this example.

This staggering amount of discrimination should be detectable in my simulated wages. And rightly enough, if I compute the gender gap between genders I discover that women make 29.89% less than men. This makes sense, as this gap represents the 10% pay cut I gave to each woman, plus an additional component driven by the discrimination in promotions. 


```python
honest_gg = data.groupby('gender').mean()
print(honest_gg['wages'], '\n')
print(' Gender gap: {}%'.format(
    np.round(100*(1- honest_gg['wages'][0]/honest_gg['wages'][1]), 2)
    ))
```

    gender
    female    6.66
    male      9.50
    Name: wages, dtype: float64 
    
     Gender gap: 29.89%
    

### "Adjusted" Gender Gaps

*Wait wait wait wait wait-a-minute!*

Says the clever pundit dude.

*Certainly you are making a naïve mistake! Certainly you can't compare pears and apples! These people are doing different jobs. Certainly you should compare the gender gap within an occupation to obtain the **true** gender gap!*

Well... Let's see what happens if we compare gender gaps *within* occupation titles. 


```python
hownotto_gg = data.groupby(['manager', 'gender']).mean()
print(hownotto_gg['wages'], '\n')

print(' Gender gap, grunts:  {}%\n'.format(
    np.round(100*(1- hownotto_gg['wages'][0][0]/hownotto_gg['wages'][0][1]), 2)
    ),
    'Gender gap, managers: {}%\n'.format(
    np.round(100*(1- hownotto_gg['wages'][1][0]/hownotto_gg['wages'][1][1]), 2)
    )
     )
```

    manager  gender
    False    female     4.05
             male       3.00
    True     female    17.10
             male      16.00
    Name: wages, dtype: float64 
    
     Gender gap, grunts:  -35.0%
     Gender gap, managers: -6.88%
    
    

Whoa! Here it shows that are actually men being discriminated against! Women make more than men on average in *each* role. Like, among non-managers, females make a staggering 35% more than men! And even among managers women outearn the men by almost 7%!

*See?* Says the clever pundit dude *It's men who need protection! We are cuddling women too much and now they exploit it and outearn men and men feel sad :(*

### Bad Controls, AKA Surtur Meets the Four Horsemen 

So, how is are these results possible when I was discriminating like a maniac just a few lines above? Well, that's because we are **controlling for an endogenous variable**, that is, job title. Because whether you are a manager or not depends not only on your ability but also on your gender, this control introduces a subtle type of bias. To appreciate the reality-warping power of bad controls, let's check the difference in ability by gender across groups.


```python
print(hownotto_gg['ability'], '\n')
```

    manager  gender
    False    female    4.5
             male      3.0
    True     female    9.5
             male      8.0
    Name: ability, dtype: float64 
    
    

And there we go. Despite men and women being on average absolutely identical in terms of ability, in this particular case we get the apparently paradoxical result that women on average outsmart men within **each occupation type**. Such is the terrifying, reality-warping power of bad controls. The Dark Side of the Force is like pre-school material in comparison.

{% raw %}
It's natural then that, on average, within each occupation group, women should earn more. What should then be the proper measure of gender gap? Well, consider that we have 10 individual of each gender, each of them a doppelganger in terms of ability of each other. So for each doppelganger couple $j\in{1,\ldots,10}$ we could compare the wage of each woman $w^{f}_{j}$ with that of her male doppelganger $w^{m}_{j}$, take the difference in wages, and average these numbers: 
{% endraw %}

{% raw %}
$$
\frac{1}{10}\sum_{j=1}^{10}(w^{m}_{j} - w^{f}_{j}) = \frac{1}{10}\sum_{j=1}^{10}w^{m}_{j} - \frac{1}{10}\sum_{j=1}^{10}w^{f}_{j}
$$
{% endraw %}

which is equal to, guess what, the raw difference in average wages, which is exactly what we computed above (29.89%).

### Conclusions

Quantifying *discrimination* (by gender, race, whatnot) in the labor market is hard. Terribly so. Don't try this at home.

Interpreting comparisons other than raw gender gaps takes training and expertise, and in most cases such comparisons just muddy the waters and make gender gaps less interpretable. The raw gender gap is instead a very simple yet powerful statistics. It's easily interpretable, and while everyone agrees it has multiple causes, it's still highly informative.

Let's stick to that 29.89%, shall we?
