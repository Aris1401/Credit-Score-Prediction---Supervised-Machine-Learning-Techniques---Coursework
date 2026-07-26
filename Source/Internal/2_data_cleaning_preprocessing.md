```python
import pandas as pd
import joblib
```


```python
credit_score = pd.read_csv('../../creditscore_anon_cw_july2023.csv')
credit_score.head()
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
      <th>A0</th>
      <th>A1</th>
      <th>A2</th>
      <th>A3</th>
      <th>A4</th>
      <th>A5</th>
      <th>A6</th>
      <th>A7</th>
      <th>A8</th>
      <th>A9</th>
      <th>...</th>
      <th>A36</th>
      <th>A37</th>
      <th>A38</th>
      <th>A39</th>
      <th>A40</th>
      <th>A41</th>
      <th>A42</th>
      <th>A43</th>
      <th>A44</th>
      <th>A45</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>28553.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10410.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>3</td>
      <td>26</td>
      <td>Female</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>7</td>
      <td>0</td>
      <td>104</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10979.06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0</td>
      <td>63</td>
      <td>Male</td>
      <td>7</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10242.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>26</td>
      <td>Male</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>200</td>
      <td>1489.00</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 46 columns</p>
</div>



# Data cleaning

The dataset seems to include a column A0 which is the ID or the row that wa can get rid of, it doesnt bring anything


```python
credit_score = credit_score.drop(columns=['A0'], axis=1)
```


```python
credit_score.head()
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
      <th>A1</th>
      <th>A2</th>
      <th>A3</th>
      <th>A4</th>
      <th>A5</th>
      <th>A6</th>
      <th>A7</th>
      <th>A8</th>
      <th>A9</th>
      <th>A10</th>
      <th>...</th>
      <th>A36</th>
      <th>A37</th>
      <th>A38</th>
      <th>A39</th>
      <th>A40</th>
      <th>A41</th>
      <th>A42</th>
      <th>A43</th>
      <th>A44</th>
      <th>A45</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>28553.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10410.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>26</td>
      <td>Female</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>7</td>
      <td>0</td>
      <td>104</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10979.06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>63</td>
      <td>Male</td>
      <td>7</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
      <td>...</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10242.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>26</td>
      <td>Male</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>200</td>
      <td>1489.00</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 45 columns</p>
</div>



# Pre-processing Pipeline

Indetifying the categorical and the numerical columns


```python
categorical_columns = ['A3', 'A4', 'A5', 'A9', 'A12', 'A16', 'A17', 'A18', 'A19', 'A20'] # Acccording to the dataset description
numerical_columns = [col for col in credit_score.columns if col not in categorical_columns and col != 'A1']

display(categorical_columns)
display(numerical_columns)
```


    ['A3', 'A4', 'A5', 'A9', 'A12', 'A16', 'A17', 'A18', 'A19', 'A20']



    ['A2',
     'A6',
     'A7',
     'A8',
     'A10',
     'A11',
     'A13',
     'A14',
     'A15',
     'A21',
     'A22',
     'A23',
     'A24',
     'A25',
     'A26',
     'A27',
     'A28',
     'A29',
     'A30',
     'A31',
     'A32',
     'A33',
     'A34',
     'A35',
     'A36',
     'A37',
     'A38',
     'A39',
     'A40',
     'A41',
     'A42',
     'A43',
     'A44',
     'A45']


Making the pre-processing pipeline


```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
```


```python
credit_score_preprocessor = ColumnTransformer(
    transformers=[
        ('num', StandardScaler(), numerical_columns),
        ('cat', OneHotEncoder(drop='first', sparse_output=False, handle_unknown='ignore'), categorical_columns)
    ]
)

credit_score_preprocessor
```




<style>#sk-container-id-1 {
  /* Definition of color scheme common for light and dark mode */
  --sklearn-color-text: #000;
  --sklearn-color-text-muted: #666;
  --sklearn-color-line: gray;
  /* Definition of color scheme for unfitted estimators */
  --sklearn-color-unfitted-level-0: #fff5e6;
  --sklearn-color-unfitted-level-1: #f6e4d2;
  --sklearn-color-unfitted-level-2: #ffe0b3;
  --sklearn-color-unfitted-level-3: chocolate;
  /* Definition of color scheme for fitted estimators */
  --sklearn-color-fitted-level-0: #f0f8ff;
  --sklearn-color-fitted-level-1: #d4ebff;
  --sklearn-color-fitted-level-2: #b3dbfd;
  --sklearn-color-fitted-level-3: cornflowerblue;

  /* Specific color for light theme */
  --sklearn-color-text-on-default-background: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, black)));
  --sklearn-color-background: var(--sg-background-color, var(--theme-background, var(--jp-layout-color0, white)));
  --sklearn-color-border-box: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, black)));
  --sklearn-color-icon: #696969;

  @media (prefers-color-scheme: dark) {
    /* Redefinition of color scheme for dark theme */
    --sklearn-color-text-on-default-background: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, white)));
    --sklearn-color-background: var(--sg-background-color, var(--theme-background, var(--jp-layout-color0, #111)));
    --sklearn-color-border-box: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, white)));
    --sklearn-color-icon: #878787;
  }
}

#sk-container-id-1 {
  color: var(--sklearn-color-text);
}

#sk-container-id-1 pre {
  padding: 0;
}

#sk-container-id-1 input.sk-hidden--visually {
  border: 0;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}

#sk-container-id-1 div.sk-dashed-wrapped {
  border: 1px dashed var(--sklearn-color-line);
  margin: 0 0.4em 0.5em 0.4em;
  box-sizing: border-box;
  padding-bottom: 0.4em;
  background-color: var(--sklearn-color-background);
}

#sk-container-id-1 div.sk-container {
  /* jupyter's `normalize.less` sets `[hidden] { display: none; }`
     but bootstrap.min.css set `[hidden] { display: none !important; }`
     so we also need the `!important` here to be able to override the
     default hidden behavior on the sphinx rendered scikit-learn.org.
     See: https://github.com/scikit-learn/scikit-learn/issues/21755 */
  display: inline-block !important;
  position: relative;
}

#sk-container-id-1 div.sk-text-repr-fallback {
  display: none;
}

div.sk-parallel-item,
div.sk-serial,
div.sk-item {
  /* draw centered vertical line to link estimators */
  background-image: linear-gradient(var(--sklearn-color-text-on-default-background), var(--sklearn-color-text-on-default-background));
  background-size: 2px 100%;
  background-repeat: no-repeat;
  background-position: center center;
}

/* Parallel-specific style estimator block */

#sk-container-id-1 div.sk-parallel-item::after {
  content: "";
  width: 100%;
  border-bottom: 2px solid var(--sklearn-color-text-on-default-background);
  flex-grow: 1;
}

#sk-container-id-1 div.sk-parallel {
  display: flex;
  align-items: stretch;
  justify-content: center;
  background-color: var(--sklearn-color-background);
  position: relative;
}

#sk-container-id-1 div.sk-parallel-item {
  display: flex;
  flex-direction: column;
}

#sk-container-id-1 div.sk-parallel-item:first-child::after {
  align-self: flex-end;
  width: 50%;
}

#sk-container-id-1 div.sk-parallel-item:last-child::after {
  align-self: flex-start;
  width: 50%;
}

#sk-container-id-1 div.sk-parallel-item:only-child::after {
  width: 0;
}

/* Serial-specific style estimator block */

#sk-container-id-1 div.sk-serial {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: var(--sklearn-color-background);
  padding-right: 1em;
  padding-left: 1em;
}


/* Toggleable style: style used for estimator/Pipeline/ColumnTransformer box that is
clickable and can be expanded/collapsed.
- Pipeline and ColumnTransformer use this feature and define the default style
- Estimators will overwrite some part of the style using the `sk-estimator` class
*/

/* Pipeline and ColumnTransformer style (default) */

#sk-container-id-1 div.sk-toggleable {
  /* Default theme specific background. It is overwritten whether we have a
  specific estimator or a Pipeline/ColumnTransformer */
  background-color: var(--sklearn-color-background);
}

/* Toggleable label */
#sk-container-id-1 label.sk-toggleable__label {
  cursor: pointer;
  display: flex;
  width: 100%;
  margin-bottom: 0;
  padding: 0.5em;
  box-sizing: border-box;
  text-align: center;
  align-items: start;
  justify-content: space-between;
  gap: 0.5em;
}

#sk-container-id-1 label.sk-toggleable__label .caption {
  font-size: 0.6rem;
  font-weight: lighter;
  color: var(--sklearn-color-text-muted);
}

#sk-container-id-1 label.sk-toggleable__label-arrow:before {
  /* Arrow on the left of the label */
  content: "▸";
  float: left;
  margin-right: 0.25em;
  color: var(--sklearn-color-icon);
}

#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {
  color: var(--sklearn-color-text);
}

/* Toggleable content - dropdown */

#sk-container-id-1 div.sk-toggleable__content {
  display: none;
  text-align: left;
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content.fitted {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content pre {
  margin: 0.2em;
  border-radius: 0.25em;
  color: var(--sklearn-color-text);
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content.fitted pre {
  /* unfitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {
  /* Expand drop-down */
  display: block;
  width: 100%;
  overflow: visible;
}

#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {
  content: "▾";
}

/* Pipeline/ColumnTransformer-specific style */

#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-label.fitted input.sk-toggleable__control:checked~label.sk-toggleable__label {
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Estimator-specific style */

/* Colorize estimator box */
#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-estimator.fitted input.sk-toggleable__control:checked~label.sk-toggleable__label {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-2);
}

#sk-container-id-1 div.sk-label label.sk-toggleable__label,
#sk-container-id-1 div.sk-label label {
  /* The background is the default theme color */
  color: var(--sklearn-color-text-on-default-background);
}

/* On hover, darken the color of the background */
#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-unfitted-level-2);
}

/* Label box, darken color on hover, fitted */
#sk-container-id-1 div.sk-label.fitted:hover label.sk-toggleable__label.fitted {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Estimator label */

#sk-container-id-1 div.sk-label label {
  font-family: monospace;
  font-weight: bold;
  display: inline-block;
  line-height: 1.2em;
}

#sk-container-id-1 div.sk-label-container {
  text-align: center;
}

/* Estimator-specific */
#sk-container-id-1 div.sk-estimator {
  font-family: monospace;
  border: 1px dotted var(--sklearn-color-border-box);
  border-radius: 0.25em;
  box-sizing: border-box;
  margin-bottom: 0.5em;
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-estimator.fitted {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

/* on hover */
#sk-container-id-1 div.sk-estimator:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-estimator.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Specification for estimator info (e.g. "i" and "?") */

/* Common style for "i" and "?" */

.sk-estimator-doc-link,
a:link.sk-estimator-doc-link,
a:visited.sk-estimator-doc-link {
  float: right;
  font-size: smaller;
  line-height: 1em;
  font-family: monospace;
  background-color: var(--sklearn-color-background);
  border-radius: 1em;
  height: 1em;
  width: 1em;
  text-decoration: none !important;
  margin-left: 0.5em;
  text-align: center;
  /* unfitted */
  border: var(--sklearn-color-unfitted-level-1) 1pt solid;
  color: var(--sklearn-color-unfitted-level-1);
}

.sk-estimator-doc-link.fitted,
a:link.sk-estimator-doc-link.fitted,
a:visited.sk-estimator-doc-link.fitted {
  /* fitted */
  border: var(--sklearn-color-fitted-level-1) 1pt solid;
  color: var(--sklearn-color-fitted-level-1);
}

/* On hover */
div.sk-estimator:hover .sk-estimator-doc-link:hover,
.sk-estimator-doc-link:hover,
div.sk-label-container:hover .sk-estimator-doc-link:hover,
.sk-estimator-doc-link:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

div.sk-estimator.fitted:hover .sk-estimator-doc-link.fitted:hover,
.sk-estimator-doc-link.fitted:hover,
div.sk-label-container:hover .sk-estimator-doc-link.fitted:hover,
.sk-estimator-doc-link.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

/* Span, style for the box shown on hovering the info icon */
.sk-estimator-doc-link span {
  display: none;
  z-index: 9999;
  position: relative;
  font-weight: normal;
  right: .2ex;
  padding: .5ex;
  margin: .5ex;
  width: min-content;
  min-width: 20ex;
  max-width: 50ex;
  color: var(--sklearn-color-text);
  box-shadow: 2pt 2pt 4pt #999;
  /* unfitted */
  background: var(--sklearn-color-unfitted-level-0);
  border: .5pt solid var(--sklearn-color-unfitted-level-3);
}

.sk-estimator-doc-link.fitted span {
  /* fitted */
  background: var(--sklearn-color-fitted-level-0);
  border: var(--sklearn-color-fitted-level-3);
}

.sk-estimator-doc-link:hover span {
  display: block;
}

/* "?"-specific style due to the `<a>` HTML tag */

#sk-container-id-1 a.estimator_doc_link {
  float: right;
  font-size: 1rem;
  line-height: 1em;
  font-family: monospace;
  background-color: var(--sklearn-color-background);
  border-radius: 1rem;
  height: 1rem;
  width: 1rem;
  text-decoration: none;
  /* unfitted */
  color: var(--sklearn-color-unfitted-level-1);
  border: var(--sklearn-color-unfitted-level-1) 1pt solid;
}

#sk-container-id-1 a.estimator_doc_link.fitted {
  /* fitted */
  border: var(--sklearn-color-fitted-level-1) 1pt solid;
  color: var(--sklearn-color-fitted-level-1);
}

/* On hover */
#sk-container-id-1 a.estimator_doc_link:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

#sk-container-id-1 a.estimator_doc_link.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-3);
}

.estimator-table summary {
    padding: .5rem;
    font-family: monospace;
    cursor: pointer;
}

.estimator-table details[open] {
    padding-left: 0.1rem;
    padding-right: 0.1rem;
    padding-bottom: 0.3rem;
}

.estimator-table .parameters-table {
    margin-left: auto !important;
    margin-right: auto !important;
}

.estimator-table .parameters-table tr:nth-child(odd) {
    background-color: #fff;
}

.estimator-table .parameters-table tr:nth-child(even) {
    background-color: #f6f6f6;
}

.estimator-table .parameters-table tr:hover {
    background-color: #e0e0e0;
}

.estimator-table table td {
    border: 1px solid rgba(106, 105, 104, 0.232);
}

.user-set td {
    color:rgb(255, 94, 0);
    text-align: left;
}

.user-set td.value pre {
    color:rgb(255, 94, 0) !important;
    background-color: transparent !important;
}

.default td {
    color: black;
    text-align: left;
}

.user-set td i,
.default td i {
    color: black;
}

.copy-paste-icon {
    background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIj48IS0tIUZvbnQgQXdlc29tZSBGcmVlIDYuNy4yIGJ5IEBmb250YXdlc29tZSAtIGh0dHBzOi8vZm9udGF3ZXNvbWUuY29tIExpY2Vuc2UgLSBodHRwczovL2ZvbnRhd2Vzb21lLmNvbS9saWNlbnNlL2ZyZWUgQ29weXJpZ2h0IDIwMjUgRm9udGljb25zLCBJbmMuLS0+PHBhdGggZD0iTTIwOCAwTDMzMi4xIDBjMTIuNyAwIDI0LjkgNS4xIDMzLjkgMTQuMWw2Ny45IDY3LjljOSA5IDE0LjEgMjEuMiAxNC4xIDMzLjlMNDQ4IDMzNmMwIDI2LjUtMjEuNSA0OC00OCA0OGwtMTkyIDBjLTI2LjUgMC00OC0yMS41LTQ4LTQ4bDAtMjg4YzAtMjYuNSAyMS41LTQ4IDQ4LTQ4ek00OCAxMjhsODAgMCAwIDY0LTY0IDAgMCAyNTYgMTkyIDAgMC0zMiA2NCAwIDAgNDhjMCAyNi41LTIxLjUgNDgtNDggNDhMNDggNTEyYy0yNi41IDAtNDgtMjEuNS00OC00OEwwIDE3NmMwLTI2LjUgMjEuNS00OCA0OC00OHoiLz48L3N2Zz4=);
    background-repeat: no-repeat;
    background-size: 14px 14px;
    background-position: 0;
    display: inline-block;
    width: 14px;
    height: 14px;
    cursor: pointer;
}
</style><body><div id="sk-container-id-1" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>ColumnTransformer(transformers=[(&#x27;num&#x27;, StandardScaler(),
                                 [&#x27;A2&#x27;, &#x27;A6&#x27;, &#x27;A7&#x27;, &#x27;A8&#x27;, &#x27;A10&#x27;, &#x27;A11&#x27;, &#x27;A13&#x27;,
                                  &#x27;A14&#x27;, &#x27;A15&#x27;, &#x27;A21&#x27;, &#x27;A22&#x27;, &#x27;A23&#x27;, &#x27;A24&#x27;,
                                  &#x27;A25&#x27;, &#x27;A26&#x27;, &#x27;A27&#x27;, &#x27;A28&#x27;, &#x27;A29&#x27;, &#x27;A30&#x27;,
                                  &#x27;A31&#x27;, &#x27;A32&#x27;, &#x27;A33&#x27;, &#x27;A34&#x27;, &#x27;A35&#x27;, &#x27;A36&#x27;,
                                  &#x27;A37&#x27;, &#x27;A38&#x27;, &#x27;A39&#x27;, &#x27;A40&#x27;, &#x27;A41&#x27;, ...]),
                                (&#x27;cat&#x27;,
                                 OneHotEncoder(drop=&#x27;first&#x27;,
                                               handle_unknown=&#x27;ignore&#x27;,
                                               sparse_output=False),
                                 [&#x27;A3&#x27;, &#x27;A4&#x27;, &#x27;A5&#x27;, &#x27;A9&#x27;, &#x27;A12&#x27;, &#x27;A16&#x27;, &#x27;A17&#x27;,
                                  &#x27;A18&#x27;, &#x27;A19&#x27;, &#x27;A20&#x27;])])</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item sk-dashed-wrapped"><div class="sk-label-container"><div class="sk-label  sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox" ><label for="sk-estimator-id-1" class="sk-toggleable__label  sk-toggleable__label-arrow"><div><div>ColumnTransformer</div></div><div><a class="sk-estimator-doc-link " rel="noreferrer" target="_blank" href="https://scikit-learn.org/1.7/modules/generated/sklearn.compose.ColumnTransformer.html">?<span>Documentation for ColumnTransformer</span></a><span class="sk-estimator-doc-link ">i<span>Not fitted</span></span></div></label><div class="sk-toggleable__content " data-param-prefix="">
        <div class="estimator-table">
            <details>
                <summary>Parameters</summary>
                <table class="parameters-table">
                  <tbody>

        <tr class="user-set">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('transformers',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">transformers&nbsp;</td>
            <td class="value">[(&#x27;num&#x27;, ...), (&#x27;cat&#x27;, ...)]</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('remainder',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">remainder&nbsp;</td>
            <td class="value">&#x27;drop&#x27;</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('sparse_threshold',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">sparse_threshold&nbsp;</td>
            <td class="value">0.3</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('n_jobs',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">n_jobs&nbsp;</td>
            <td class="value">None</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('transformer_weights',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">transformer_weights&nbsp;</td>
            <td class="value">None</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('verbose',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">verbose&nbsp;</td>
            <td class="value">False</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('verbose_feature_names_out',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">verbose_feature_names_out&nbsp;</td>
            <td class="value">True</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('force_int_remainder_cols',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">force_int_remainder_cols&nbsp;</td>
            <td class="value">&#x27;deprecated&#x27;</td>
        </tr>

                  </tbody>
                </table>
            </details>
        </div>
    </div></div></div><div class="sk-parallel"><div class="sk-parallel-item"><div class="sk-item"><div class="sk-label-container"><div class="sk-label  sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-2" type="checkbox" ><label for="sk-estimator-id-2" class="sk-toggleable__label  sk-toggleable__label-arrow"><div><div>num</div></div></label><div class="sk-toggleable__content " data-param-prefix="num__"><pre>[&#x27;A2&#x27;, &#x27;A6&#x27;, &#x27;A7&#x27;, &#x27;A8&#x27;, &#x27;A10&#x27;, &#x27;A11&#x27;, &#x27;A13&#x27;, &#x27;A14&#x27;, &#x27;A15&#x27;, &#x27;A21&#x27;, &#x27;A22&#x27;, &#x27;A23&#x27;, &#x27;A24&#x27;, &#x27;A25&#x27;, &#x27;A26&#x27;, &#x27;A27&#x27;, &#x27;A28&#x27;, &#x27;A29&#x27;, &#x27;A30&#x27;, &#x27;A31&#x27;, &#x27;A32&#x27;, &#x27;A33&#x27;, &#x27;A34&#x27;, &#x27;A35&#x27;, &#x27;A36&#x27;, &#x27;A37&#x27;, &#x27;A38&#x27;, &#x27;A39&#x27;, &#x27;A40&#x27;, &#x27;A41&#x27;, &#x27;A42&#x27;, &#x27;A43&#x27;, &#x27;A44&#x27;, &#x27;A45&#x27;]</pre></div></div></div><div class="sk-serial"><div class="sk-item"><div class="sk-estimator  sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-3" type="checkbox" ><label for="sk-estimator-id-3" class="sk-toggleable__label  sk-toggleable__label-arrow"><div><div>StandardScaler</div></div><div><a class="sk-estimator-doc-link " rel="noreferrer" target="_blank" href="https://scikit-learn.org/1.7/modules/generated/sklearn.preprocessing.StandardScaler.html">?<span>Documentation for StandardScaler</span></a></div></label><div class="sk-toggleable__content " data-param-prefix="num__">
        <div class="estimator-table">
            <details>
                <summary>Parameters</summary>
                <table class="parameters-table">
                  <tbody>

        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('copy',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">copy&nbsp;</td>
            <td class="value">True</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('with_mean',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">with_mean&nbsp;</td>
            <td class="value">True</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('with_std',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">with_std&nbsp;</td>
            <td class="value">True</td>
        </tr>

                  </tbody>
                </table>
            </details>
        </div>
    </div></div></div></div></div></div><div class="sk-parallel-item"><div class="sk-item"><div class="sk-label-container"><div class="sk-label  sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-4" type="checkbox" ><label for="sk-estimator-id-4" class="sk-toggleable__label  sk-toggleable__label-arrow"><div><div>cat</div></div></label><div class="sk-toggleable__content " data-param-prefix="cat__"><pre>[&#x27;A3&#x27;, &#x27;A4&#x27;, &#x27;A5&#x27;, &#x27;A9&#x27;, &#x27;A12&#x27;, &#x27;A16&#x27;, &#x27;A17&#x27;, &#x27;A18&#x27;, &#x27;A19&#x27;, &#x27;A20&#x27;]</pre></div></div></div><div class="sk-serial"><div class="sk-item"><div class="sk-estimator  sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-5" type="checkbox" ><label for="sk-estimator-id-5" class="sk-toggleable__label  sk-toggleable__label-arrow"><div><div>OneHotEncoder</div></div><div><a class="sk-estimator-doc-link " rel="noreferrer" target="_blank" href="https://scikit-learn.org/1.7/modules/generated/sklearn.preprocessing.OneHotEncoder.html">?<span>Documentation for OneHotEncoder</span></a></div></label><div class="sk-toggleable__content " data-param-prefix="cat__">
        <div class="estimator-table">
            <details>
                <summary>Parameters</summary>
                <table class="parameters-table">
                  <tbody>

        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('categories',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">categories&nbsp;</td>
            <td class="value">&#x27;auto&#x27;</td>
        </tr>


        <tr class="user-set">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('drop',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">drop&nbsp;</td>
            <td class="value">&#x27;first&#x27;</td>
        </tr>


        <tr class="user-set">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('sparse_output',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">sparse_output&nbsp;</td>
            <td class="value">False</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('dtype',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">dtype&nbsp;</td>
            <td class="value">&lt;class &#x27;numpy.float64&#x27;&gt;</td>
        </tr>


        <tr class="user-set">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('handle_unknown',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">handle_unknown&nbsp;</td>
            <td class="value">&#x27;ignore&#x27;</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('min_frequency',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">min_frequency&nbsp;</td>
            <td class="value">None</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('max_categories',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">max_categories&nbsp;</td>
            <td class="value">None</td>
        </tr>


        <tr class="default">
            <td><i class="copy-paste-icon"
                 onclick="copyToClipboard('feature_name_combiner',
                          this.parentElement.nextElementSibling)"
            ></i></td>
            <td class="param">feature_name_combiner&nbsp;</td>
            <td class="value">&#x27;concat&#x27;</td>
        </tr>

                  </tbody>
                </table>
            </details>
        </div>
    </div></div></div></div></div></div></div></div></div></div><script>function copyToClipboard(text, element) {
    // Get the parameter prefix from the closest toggleable content
    const toggleableContent = element.closest('.sk-toggleable__content');
    const paramPrefix = toggleableContent ? toggleableContent.dataset.paramPrefix : '';
    const fullParamName = paramPrefix ? `${paramPrefix}${text}` : text;

    const originalStyle = element.style;
    const computedStyle = window.getComputedStyle(element);
    const originalWidth = computedStyle.width;
    const originalHTML = element.innerHTML.replace('Copied!', '');

    navigator.clipboard.writeText(fullParamName)
        .then(() => {
            element.style.width = originalWidth;
            element.style.color = 'green';
            element.innerHTML = "Copied!";

            setTimeout(() => {
                element.innerHTML = originalHTML;
                element.style = originalStyle;
            }, 2000);
        })
        .catch(err => {
            console.error('Failed to copy:', err);
            element.style.color = 'red';
            element.innerHTML = "Failed!";
            setTimeout(() => {
                element.innerHTML = originalHTML;
                element.style = originalStyle;
            }, 2000);
        });
    return false;
}

document.querySelectorAll('.fa-regular.fa-copy').forEach(function(element) {
    const toggleableContent = element.closest('.sk-toggleable__content');
    const paramPrefix = toggleableContent ? toggleableContent.dataset.paramPrefix : '';
    const paramName = element.parentElement.nextElementSibling.textContent.trim();
    const fullParamName = paramPrefix ? `${paramPrefix}${paramName}` : paramName;

    element.setAttribute('title', fullParamName);
});
</script></body>




```python
joblib.dump(credit_score_preprocessor, './Data/credit_score_preprocessor.pkl')
```




    ['./Data/credit_score_preprocessor.pkl']



# Addressing the missing values in the target feature

Training a random forest classifier to impute the dataset


```python
from sklearn.pipeline import Pipeline
from sklearn.ensemble import RandomForestClassifier
```


```python
imputer_pipeline = Pipeline(steps=[
    ('preprocessor', credit_score_preprocessor),
    ('imputer_model', RandomForestClassifier(n_estimators=100, class_weight='balanced_subsample', random_state=42))
])
```


```python
rated_data = credit_score[credit_score['A1'] != 0]
unrated_data = credit_score[credit_score['A1'] == 0]

rated_data
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
      <th>A1</th>
      <th>A2</th>
      <th>A3</th>
      <th>A4</th>
      <th>A5</th>
      <th>A6</th>
      <th>A7</th>
      <th>A8</th>
      <th>A9</th>
      <th>A10</th>
      <th>...</th>
      <th>A36</th>
      <th>A37</th>
      <th>A38</th>
      <th>A39</th>
      <th>A40</th>
      <th>A41</th>
      <th>A42</th>
      <th>A43</th>
      <th>A44</th>
      <th>A45</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>28553.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10410.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>26</td>
      <td>Female</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>7</td>
      <td>0</td>
      <td>104</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10979.06</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>10</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>500</td>
      <td>9163.00</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4</td>
      <td>37</td>
      <td>Male</td>
      <td>4</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>24</td>
      <td>...</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1587.00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1852</th>
      <td>4</td>
      <td>37</td>
      <td>Female</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>12</td>
      <td>...</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6127.15</td>
    </tr>
    <tr>
      <th>1853</th>
      <td>3</td>
      <td>27</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>12</td>
      <td>...</td>
      <td>14</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>1956.00</td>
    </tr>
    <tr>
      <th>1857</th>
      <td>3</td>
      <td>36</td>
      <td>Female</td>
      <td>5</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>24</td>
      <td>...</td>
      <td>31</td>
      <td>14</td>
      <td>0</td>
      <td>28</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>4</td>
      <td>650</td>
      <td>43925.00</td>
    </tr>
    <tr>
      <th>1858</th>
      <td>2</td>
      <td>29</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>12</td>
      <td>...</td>
      <td>1</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>9578.89</td>
    </tr>
    <tr>
      <th>1862</th>
      <td>4</td>
      <td>23</td>
      <td>Male</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>83</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>500</td>
      <td>4846.00</td>
    </tr>
  </tbody>
</table>
<p>476 rows × 45 columns</p>
</div>




```python
imputer_pipeline.fit(
    rated_data.drop(columns=['A1']),
    rated_data['A1']
)

predicted_a1 = imputer_pipeline.predict(unrated_data.drop(columns=['A1']))
```

    C:\Users\cesta\AppData\Roaming\Python\Python313\site-packages\sklearn\preprocessing\_encoders.py:246: UserWarning: Found unknown categories in columns [5] during transform. These unknown categories will be encoded as all zeros
      warnings.warn(
    


```python
credit_score_imputed = credit_score.copy()
credit_score_imputed.loc[credit_score_imputed['A1'] == 0, 'A1'] = predicted_a1
```


```python
credit_score_imputed.head()
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
      <th>A1</th>
      <th>A2</th>
      <th>A3</th>
      <th>A4</th>
      <th>A5</th>
      <th>A6</th>
      <th>A7</th>
      <th>A8</th>
      <th>A9</th>
      <th>A10</th>
      <th>...</th>
      <th>A36</th>
      <th>A37</th>
      <th>A38</th>
      <th>A39</th>
      <th>A40</th>
      <th>A41</th>
      <th>A42</th>
      <th>A43</th>
      <th>A44</th>
      <th>A45</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>28553.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10410.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>26</td>
      <td>Female</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>7</td>
      <td>0</td>
      <td>104</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10979.06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>63</td>
      <td>Male</td>
      <td>7</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
      <td>...</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10242.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>26</td>
      <td>Male</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>200</td>
      <td>1489.00</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 45 columns</p>
</div>




```python
print("Target A1 Distribution After Imputation:")
display(credit_score_imputed['A1'].value_counts().sort_index())
```

    Target A1 Distribution After Imputation:
    


    A1
    1       6
    2      32
    3     124
    4    1690
    5      15
    Name: count, dtype: int64


Results show that compared to the original and after imputation using random forest, since in the non imputed data the class 4 still domintad the fitting was unbalanced making the predictions biased towards the class 4. We need to find other way of imputation

Imputation using KNN


```python
from sklearn.pipeline import Pipeline
from sklearn.neighbors import KNeighborsClassifier
```


```python
knn_imputer_pipeline = Pipeline(steps=[
    ('preprocessor', credit_score_preprocessor),
    ('imputer_model', KNeighborsClassifier(n_neighbors=3, weights='distance'))
])

X_rated = rated_data.drop(columns=['A1'])
y_rated = rated_data['A1']
X_unrated = unrated_data.drop(columns=['A1'])
```


```python
knn_imputer_pipeline.fit(X_rated, y_rated)
predicted_a1_knn = knn_imputer_pipeline.predict(X_unrated)
```

    C:\Users\cesta\AppData\Roaming\Python\Python313\site-packages\sklearn\preprocessing\_encoders.py:246: UserWarning: Found unknown categories in columns [5] during transform. These unknown categories will be encoded as all zeros
      warnings.warn(
    


```python
credit_score_imputed = credit_score.copy()
credit_score_imputed.loc[credit_score_imputed['A1'] == 0, 'A1'] = predicted_a1_knn

print("--- KNN Similarity Imputation Breakdown ---")
display(credit_score_imputed['A1'].value_counts().sort_index())
```

    --- KNN Similarity Imputation Breakdown ---
    


    A1
    1       8
    2      56
    3     260
    4    1515
    5      28
    Name: count, dtype: int64


Using KNN hasn't also been really fructuous since the classes are still imbalanced, this can still lead to some bas when trining the model

Rank-Based Quantile Binning (Continuous Rating Index)


```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.svm import SVR
from sklearn.pipeline import Pipeline
```


```python
regressor_pipeline = Pipeline(steps=[
    ('preprocessor', credit_score_preprocessor),
    ('regressor', SVR())
])
```


```python
rated_data = credit_score[credit_score['A1'] != 0]
unrated_data = credit_score[credit_score['A1'] == 0]

regressor_pipeline.fit(
    rated_data.drop(columns=['A1']),
    rated_data['A1']
)

unrated_scores = regressor_pipeline.predict(unrated_data.drop(columns=['A1']))
```

    C:\Users\cesta\AppData\Roaming\Python\Python313\site-packages\sklearn\preprocessing\_encoders.py:246: UserWarning: Found unknown categories in columns [5] during transform. These unknown categories will be encoded as all zeros
      warnings.warn(
    


```python
unrated_scores
```




    array([3.51456124, 3.85877432, 3.6298599 , ..., 3.3795493 , 3.3401109 ,
           3.91135076], shape=(1391,))




```python

quantiles = [0, 0.012, 0.077, 0.289, 0.968, 1.0]
predicted_a1_binned = pd.qcut(unrated_scores, q=quantiles, labels=[1, 2, 3, 4, 5])

# Apply back to dataset
credit_score_imputed = credit_score.copy()
credit_score_imputed.loc[credit_score_imputed['A1'] == 0, 'A1'] = predicted_a1_binned

print("--- Quantile-Binned Imputation Breakdown ---")
display(credit_score_imputed['A1'].value_counts().sort_index())
```

    --- Quantile-Binned Imputation Breakdown ---
    


    A1
    1      23
    2     131
    3     386
    4    1267
    5      60
    Name: count, dtype: int64


Using a manual approach, which consists of predicting using a regressor then binning the values to target classes, also didn't work out so let's find other solutions.

Using SMOTE


```python
from imblearn.over_sampling import SMOTE
from sklearn.ensemble import RandomForestClassifier
from sklearn.neighbors import KNeighborsClassifier
```


```python

X_processed = credit_score_preprocessor.fit_transform(credit_score.drop(columns=['A1']))
y = credit_score['A1']

mask_rated = (y != 0)
X_rated = X_processed[mask_rated]
y_rated = y[mask_rated]
X_unrated = X_processed[~mask_rated]
```


```python

smote = SMOTE(k_neighbors=5, random_state=42)
X_rated_smote, y_rated_smote = smote.fit_resample(X_rated, y_rated)

display(pd.Series(y_rated_smote).value_counts().sort_index())
```


    A1
    1    323
    2    323
    3    323
    4    323
    5    323
    Name: count, dtype: int64



```python

rf_imputer = RandomForestClassifier(n_estimators=100, random_state=42)
rf_imputer.fit(X_rated_smote, y_rated_smote)
rf_predictions = rf_imputer.predict(X_unrated)

df_rf = credit_score.copy()
df_rf.loc[df_rf['A1'] == 0, 'A1'] = rf_predictions
```


```python
knn_imputer = KNeighborsClassifier(n_neighbors=5, weights='distance')
knn_imputer.fit(X_rated_smote, y_rated_smote)
knn_predictions = knn_imputer.predict(X_unrated)

df_knn = credit_score.copy()
df_knn.loc[df_knn['A1'] == 0, 'A1'] = knn_predictions
```


```python

imputation_comparison = pd.DataFrame({
    'Original Known (476)': y_rated.value_counts().sort_index(),
    'SMOTE + Random Forest (1,867)': df_rf['A1'].value_counts().sort_index(),
    'SMOTE + KNN (1,867)': df_knn['A1'].value_counts().sort_index()
})

print("\n--- Imputation Comparison ---")
display(imputation_comparison)
```

    
    --- Imputation Comparison ---
    


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
      <th>Original Known (476)</th>
      <th>SMOTE + Random Forest (1,867)</th>
      <th>SMOTE + KNN (1,867)</th>
    </tr>
    <tr>
      <th>A1</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>6</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>31</td>
      <td>44</td>
      <td>165</td>
    </tr>
    <tr>
      <th>3</th>
      <td>101</td>
      <td>181</td>
      <td>571</td>
    </tr>
    <tr>
      <th>4</th>
      <td>323</td>
      <td>1616</td>
      <td>962</td>
    </tr>
    <tr>
      <th>5</th>
      <td>15</td>
      <td>20</td>
      <td>155</td>
    </tr>
  </tbody>
</table>
</div>


After, re-distributing the data using SMOTE, and then predicting the classes using a classifier, we've came to a somewhat usable result using KNN over Random Forest Classifier. This resulted in KNN distributing the classes better than Random Forest so we can take this result.

Storing the dataset


```python
credit_score_imputed = df_knn.copy()
```


```python
credit_score_imputed.head()
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
      <th>A1</th>
      <th>A2</th>
      <th>A3</th>
      <th>A4</th>
      <th>A5</th>
      <th>A6</th>
      <th>A7</th>
      <th>A8</th>
      <th>A9</th>
      <th>A10</th>
      <th>...</th>
      <th>A36</th>
      <th>A37</th>
      <th>A38</th>
      <th>A39</th>
      <th>A40</th>
      <th>A41</th>
      <th>A42</th>
      <th>A43</th>
      <th>A44</th>
      <th>A45</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>28553.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>31</td>
      <td>Female</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10410.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>26</td>
      <td>Female</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>0</td>
      <td>7</td>
      <td>0</td>
      <td>104</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10979.06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>63</td>
      <td>Male</td>
      <td>7</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
      <td>...</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10242.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>26</td>
      <td>Male</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>24</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>200</td>
      <td>1489.00</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 45 columns</p>
</div>




```python
credit_score_imputed.to_csv('./Data/credit_score_imputed.csv', index=False)
```


```python

```
