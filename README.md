Download Link: https://assignmentchef.com/product/solved-fys-stk4155-project1-regression-analysis-and-resampling-methods
<br>
<h2>Regression analysis and resampling methods</h2>

The main aim of this project is to study in more detail various regression methods, including the Ordinary Least Squares (OLS) method, Ridge regression and finally Lasso regression. Ridge regression will be discussed during the Friday lecture of week 36 while Lasso Regression will be discussed during the lectures of week 37.

The methods are in turn combined with resampling techniques like the bootstrap method and cross validation. These are discussed during weeks 36 and 37.

We will first study how to fit polynomials to a specific two-dimensional function called <a href="http://www.dtic.mil/dtic/tr/fulltext/u2/a081688.pdf">Franke’s function</a>. This is a function which has been widely used when testing various interpolation and fitting algorithms. Furthermore, after having established the model and the method, we will employ resamling techniques such as cross-validation and/or bootstrap in order to perform a proper assessment of our models. We will also study in detail the so-called Bias-Variance trade off.

The Franke function, which is a weighted sum of four exponentials reads as follows

<em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot; display=&quot;block&quot;><mtable columnalign=&quot;right left right left right left right left right left right left&quot; rowspacing=&quot;3pt&quot; columnspacing=&quot;0em 2em 0em 2em 0em 2em 0em 2em 0em 2em 0em&quot; displaystyle=&quot;true&quot;><mtr><mtd><mi>f</mi><mo stretchy=&quot;false&quot;>(</mo><mi>x</mi><mo>,</mo><mi>y</mi><mo stretchy=&quot;false&quot;>)</mo></mtd><mtd><mi></mi><mo>=</mo><mfrac><mn>3</mn><mn>4</mn></mfrac><mi>exp</mi><mo>&amp;#x2061;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mrow><mo>(</mo><mrow><mo>&amp;#x2212;</mo><mfrac><mrow><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>x</mi><mo>&amp;#x2212;</mo><mn>2</mn><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mn>4</mn></mfrac><mo>&amp;#x2212;</mo><mfrac><mrow><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>y</mi><mo>&amp;#x2212;</mo><mn>2</mn><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mn>4</mn></mfrac></mrow><mo>)</mo></mrow></mrow><mo>+</mo><mfrac><mn>3</mn><mn>4</mn></mfrac><mi>exp</mi><mo>&amp;#x2061;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mrow><mo>(</mo><mrow><mo>&amp;#x2212;</mo><mfrac><mrow><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>x</mi><mo>+</mo><mn>1</mn><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mn>49</mn></mfrac><mo>&amp;#x2212;</mo><mfrac><mrow><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>y</mi><mo>+</mo><mn>1</mn><mo stretchy=&quot;false&quot;>)</mo></mrow><mn>10</mn></mfrac></mrow><mo>)</mo></mrow></mrow></mtd></mtr><mtr><mtd /><mtd><mi></mi><mo>+</mo><mfrac><mn>1</mn><mn>2</mn></mfrac><mi>exp</mi><mo>&amp;#x2061;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mrow><mo>(</mo><mrow><mo>&amp;#x2212;</mo><mfrac><mrow><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>x</mi><mo>&amp;#x2212;</mo><mn>7</mn><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mn>4</mn></mfrac><mo>&amp;#x2212;</mo><mfrac><mrow><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>y</mi><mo>&amp;#x2212;</mo><mn>3</mn><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mn>4</mn></mfrac></mrow><mo>)</mo></mrow></mrow><mo>&amp;#x2212;</mo><mfrac><mn>1</mn><mn>5</mn></mfrac><mi>exp</mi><mo>&amp;#x2061;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mrow><mo>(</mo><mrow><mo>&amp;#x2212;</mo><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>x</mi><mo>&amp;#x2212;</mo><mn>4</mn><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup><mo>&amp;#x2212;</mo><mo stretchy=&quot;false&quot;>(</mo><mn>9</mn><mi>y</mi><mo>&amp;#x2212;</mo><mn>7</mn><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mo>)</mo></mrow></mrow><mo>.</mo></mtd></mtr></mtable></math>">f</span></em>(<em>x</em>,<em>y</em>)=34exp(−(9<em>x</em>−2)24−(9<em>y</em>−2)24)+34exp(−(9<em>x</em>+1)249−(9<em>y</em>+1)10)+12exp(−(9<em>x</em>−7)24−(9<em>y</em>−3)24)−15exp(−(9<em>x</em>−4)2−(9<em>y</em>−7)2).f(x,y)=34exp⁡(−(9x−2)24−(9y−2)24)+34exp⁡(−(9x+1)249−(9y+1)10)+12exp⁡(−(9x−7)24−(9y−3)24)−15exp⁡(−(9x−4)2−(9y−7)2).

The function will be defined for <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>x</mi><mo>,</mo><mi>y</mi><mo>&amp;#x2208;</mo><mo stretchy=&quot;false&quot;>[</mo><mn>0</mn><mo>,</mo><mn>1</mn><mo stretchy=&quot;false&quot;>]</mo></math>">x</span></em>,<em>y</em>∈[0,1]x,y∈[0,1]. Our first step will be to perform an OLS regression analysis of this function, trying out a polynomial fit with an <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>x</mi></math>">x</span></em>x and <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>y</mi></math>">y</span></em>y dependence of the form <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mo stretchy=&quot;false&quot;>[</mo><mi>x</mi><mo>,</mo><mi>y</mi><mo>,</mo><msup><mi>x</mi><mn>2</mn></msup><mo>,</mo><msup><mi>y</mi><mn>2</mn></msup><mo>,</mo><mi>x</mi><mi>y</mi><mo>,</mo><mo>&amp;#x2026;</mo><mo stretchy=&quot;false&quot;>]</mo></math>">[<em>x</em>,<em>y</em>,<em>x</em>2</span>,<em>y</em>2,<em>xy</em>,…][x,y,x2,y2,xy,…]. We will also include bootstrap first as a resampling technique. After that we will include the cross-validation technique. As in homeworks 1 and 2, we can use a uniform distribution to set up the arrays of values for <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>x</mi></math>">x</span></em>x and <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>y</mi></math>">y</span></em>y, or as in the example below just a set of fixed values for <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>x</mi></math>">x</span></em>x and <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>y</mi></math>">y</span></em>y with a given step size. We will fit a function (for example a polynomial) of <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>x</mi></math>">x</span></em>x and <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>y</mi></math>">y</span></em>y. Thereafter we will repeat much of the same procedure using the Ridge and Lasso regression methods, introducing thus a dependence on the bias (penalty) <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>&amp;#x03BB;</mi></math>">λ</span></em>λ.

Finally we are going to use (real) digital terrain data and try to reproduce these data using the same methods. We will also try to go beyond the second-order polynomials metioned above and explore which polynomial fits the data best.

The Python code for the Franke function is included here (it performs also a three-dimensional plot of it)

<strong>from</strong> <strong>mpl_toolkits.mplot3d</strong> <strong>import</strong> Axes3D<strong>import</strong> <strong>matplotlib.pyplot</strong> <strong>as</strong> <strong>plt</strong><strong>from</strong> <strong>matplotlib</strong> <strong>import</strong> cm<strong>from</strong> <strong>matplotlib.ticker</strong> <strong>import</strong> LinearLocator, FormatStrFormatter<strong>import</strong> <strong>numpy</strong> <strong>as</strong> <strong>np</strong><strong>from</strong> <strong>random</strong> <strong>import</strong> random, seed fig = plt.figure()ax = fig.gca(projection=’3d’) <em># Make data.</em>x = np.arange(0, 1, 0.05)y = np.arange(0, 1, 0.05)x, y = np.meshgrid(x,y)  <strong>def</strong> FrankeFunction(x,y):    term1 = 0.75*np.exp(-(0.25*(9*x-2)**2) – 0.25*((9*y-2)**2))    term2 = 0.75*np.exp(-((9*x+1)**2)/49.0 – 0.1*(9*y+1))    term3 = 0.5*np.exp(-(9*x-7)**2/4.0 – 0.25*((9*y-3)**2))    term4 = -0.2*np.exp(-(9*x-4)**2 – (9*y-7)**2)    <strong>return</strong> term1 + term2 + term3 + term4  z = FrankeFunction(x, y) <em># Plot the surface.</em>surf = ax.plot_surface(x, y, z, cmap=cm.coolwarm,                       linewidth=0, antialiased=<strong>False</strong>) <em># Customize the z axis.</em>ax.set_zlim(-0.10, 1.40)ax.zaxis.set_major_locator(LinearLocator(10))ax.zaxis.set_major_formatter(FormatStrFormatter(‘<strong>%.02f</strong>‘)) <em># Add a color bar which maps values to colors.</em>fig.colorbar(surf, shrink=0.5, aspect=5) plt.show()

<h3>Part a): Ordinary Least Square (OLS) on the Franke function</h3>

We will generate our own dataset for a function <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi mathvariant=&quot;normal&quot;>F</mi><mi mathvariant=&quot;normal&quot;>r</mi><mi mathvariant=&quot;normal&quot;>a</mi><mi mathvariant=&quot;normal&quot;>n</mi><mi mathvariant=&quot;normal&quot;>k</mi><mi mathvariant=&quot;normal&quot;>e</mi><mi mathvariant=&quot;normal&quot;>F</mi><mi mathvariant=&quot;normal&quot;>u</mi><mi mathvariant=&quot;normal&quot;>n</mi><mi mathvariant=&quot;normal&quot;>c</mi><mi mathvariant=&quot;normal&quot;>t</mi><mi mathvariant=&quot;normal&quot;>i</mi><mi mathvariant=&quot;normal&quot;>o</mi><mi mathvariant=&quot;normal&quot;>n</mi></mrow><mo stretchy=&quot;false&quot;>(</mo><mi>x</mi><mo>,</mo><mi>y</mi><mo stretchy=&quot;false&quot;>)</mo></math>">FrankeFunction(<em>x</em>,<em>y</em>)</span>FrankeFunction(x,y) with <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>x</mi><mo>,</mo><mi>y</mi><mo>&amp;#x2208;</mo><mo stretchy=&quot;false&quot;>[</mo><mn>0</mn><mo>,</mo><mn>1</mn><mo stretchy=&quot;false&quot;>]</mo></math>">x</span></em>,<em>y</em>∈[0,1]x,y∈[0,1]. The function <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>f</mi><mo stretchy=&quot;false&quot;>(</mo><mi>x</mi><mo>,</mo><mi>y</mi><mo stretchy=&quot;false&quot;>)</mo></math>">f</span></em>(<em>x</em>,<em>y</em>)f(x,y) is the Franke function. You should explore also the addition of an added stochastic noise to this function using the normal distribution <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot;>N</mi></mrow><mo class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot; stretchy=&quot;false&quot;>(</mo><mn class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot;>0</mn><mo class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot;>,</mo><mn class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot;>1</mn><mo class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot; stretchy=&quot;false&quot;>)</mo></math>">N(0,1)</span>N(0,1).

<em>Write your own code</em> (using either a matrix inversion or a singular value decomposition from e.g., <strong>numpy</strong> ) or use your code from homeworks 1 and 2 and perform a standard least square regression analysis using polynomials in <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>x</mi></math>">x</span></em>x and <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>y</mi></math>">y</span></em>y up to fifth order. Find the <a href="https://en.wikipedia.org/wiki/Confidence_interval">confidence intervals</a> of the parameters (estimators) <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>&amp;#x03B2;</mi></math>">β</span></em>β by computing their variances, evaluate the Mean Squared error (MSE)

<em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot; display=&quot;block&quot;><mi>M</mi><mi>S</mi><mi>E</mi><mo stretchy=&quot;false&quot;>(</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x005E;</mo></mover></mrow><mo>,</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mo stretchy=&quot;false&quot;>&amp;#x005E;</mo></mover></mrow><mo stretchy=&quot;false&quot;>)</mo><mo>=</mo><mfrac><mn>1</mn><mi>n</mi></mfrac><munderover><mo>&amp;#x2211;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>i</mi><mo>=</mo><mn>0</mn></mrow><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>n</mi><mo>&amp;#x2212;</mo><mn>1</mn></mrow></munderover><mo stretchy=&quot;false&quot;>(</mo><msub><mi>y</mi><mi>i</mi></msub><mo>&amp;#x2212;</mo><msub><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mi>i</mi></msub><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup><mo>,</mo></math>">MSE</span></em>(<em>y</em>^,<em>y</em>~^)=1<em>n</em>∑<em>i</em>=0<em>n</em>−1(<em>y</em>i−<em>y</em>~<em>i</em>)2,MSE(y^,y~^)=1n∑i=0n−1(yi−y~i)2,

and the <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msup><mi>R</mi><mn>2</mn></msup></math>">R</span></em>2R2 score function. If <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msub><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x005E;</mo></mover></mrow><mo stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mi>i</mi></msub></math>">y</span></em>^~<em>i</em>y^~i is the predicted value of the <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>i</mi><mo>&amp;#x2212;</mo><mi>t</mi><mi>h</mi></math>">i</span></em>−<em>th</em>i−th sample and <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msub><mi>y</mi><mi>i</mi></msub></math>">y</span></em>iyi is the corresponding true value, then the score <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msup><mi>R</mi><mn>2</mn></msup></math>">R</span></em>2R2 is defined as

<em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot; display=&quot;block&quot;><msup><mi>R</mi><mn>2</mn></msup><mo stretchy=&quot;false&quot;>(</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x005E;</mo></mover></mrow><mo>,</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x005E;</mo></mover></mrow><mo stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mo stretchy=&quot;false&quot;>)</mo><mo>=</mo><mn>1</mn><mo>&amp;#x2212;</mo><mfrac><mrow><munderover><mo>&amp;#x2211;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>i</mi><mo>=</mo><mn>0</mn></mrow><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>n</mi><mo>&amp;#x2212;</mo><mn>1</mn></mrow></munderover><mo stretchy=&quot;false&quot;>(</mo><msub><mi>y</mi><mi>i</mi></msub><mo>&amp;#x2212;</mo><msub><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mi>i</mi></msub><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mrow><munderover><mo>&amp;#x2211;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>i</mi><mo>=</mo><mn>0</mn></mrow><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>n</mi><mo>&amp;#x2212;</mo><mn>1</mn></mrow></munderover><mo stretchy=&quot;false&quot;>(</mo><msub><mi>y</mi><mi>i</mi></msub><mo>&amp;#x2212;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x00AF;</mo></mover></mrow><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow></mfrac><mo>,</mo></math>">R</span></em>2(<em>y</em>^,<em>y</em>^~)=1−∑<em>n</em>−1<em>i</em>=0(<em>y</em>i−<em>y</em>~<em>i</em>)2∑<em>n</em>−1<em>i</em>=0(<em>y</em>i−<em>y</em>¯)2,R2(y^,y^~)=1−∑i=0n−1(yi−y~i)2∑i=0n−1(yi−y¯)2,

where we have defined the mean value of <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x005E;</mo></mover></mrow></math>">y</span></em>^y^ as

<em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot; display=&quot;block&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x00AF;</mo></mover></mrow><mo>=</mo><mfrac><mn>1</mn><mi>n</mi></mfrac><munderover><mo>&amp;#x2211;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>i</mi><mo>=</mo><mn>0</mn></mrow><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>n</mi><mo>&amp;#x2212;</mo><mn>1</mn></mrow></munderover><msub><mi>y</mi><mi>i</mi></msub><mo>.</mo></math>">y</span></em>¯=1<em>n</em>∑<em>i</em>=0<em>n</em>−1yi.y¯=1n∑i=0n−1yi.

Your code has to include a scaling of the data (for example by subtracting the mean value, see also <a href="https://compphysics.github.io/MachineLearning/doc/Projects/2020/hw2/html/hw2-bs.html">homework set 2</a> for examples) and a split of the data in training and test data. For this part you can either write your own code or use for example the function for splitting training data provided by the library <strong>Scikit-Learn</strong> (make sure you have installed it). This function is called <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>t</mi><mi>r</mi><mi>a</mi><mi>i</mi><mi>n</mi><mi mathvariant=&quot;normal&quot;>&amp;#x005F;</mi><mi>t</mi><mi>e</mi><mi>s</mi><mi>t</mi><mi mathvariant=&quot;normal&quot;>&amp;#x005F;</mi><mi>s</mi><mi>p</mi><mi>l</mi><mi>i</mi><mi>t</mi></math>">train</span></em>_<em>test</em>_<em>split</em>train_test_split. Similarly, and see the solution to <a href="https://compphysics.github.io/MachineLearning/doc/Projects/2020/hw2/html/hw2-bs.html">homework set 2, exercise 2</a>, you can use the data normalization functionality of <strong>Scikit-Learn</strong>.

It is normal in essentially all Machine Learning studies to split the data in a training set and a test set (eventually also an additional validation set). There is no explicit recipe for how much data should be included as training data and say test data. An accepted rule of thumb is to use approximately <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mn>2</mn><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mo>/</mo></mrow><mn>3</mn></math>">2/3</span>2/3 to <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mn>4</mn><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mo>/</mo></mrow><mn>5</mn></math>">4/5</span>4/5 of the data as training data.

<h3>Part b): Bias-variance trade-off and resamplng techniques</h3>

Our aim here is to study the bias-variance trade-off by implementing the <strong>bootstrap</strong> resampling technique.

With a code which does OLS and includes resampling techniques, we will now discuss the bias-variance trade-off in the context of continuous predictions such as regression. However, many of the intuitions and ideas discussed here also carry over to classification tasks and basically all Machine Learning algorithms.

Before you perform an analysis of the bias-variance trade-off on your test data, make first a figure similar to Fig. 2.11 of Hastie, Tibshirani, and Friedman. Figure 2.11 of this reference displays only the test and training MSEs. The test MSE can be used to indicate possible regions of low/high bias and variance. You will most likely not get an equally smooth curve!

With this result we move on to the bias-variance trade-off analysis.

Consider a dataset <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot;>L</mi></mrow></math>">L</span>L consisting of the data <strong><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msub><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi mathvariant=&quot;bold&quot;>X</mi></mrow><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi class=&quot;MJX-tex-caligraphic&quot; mathvariant=&quot;script&quot;>L</mi></mrow></msub><mo>=</mo><mo fence=&quot;false&quot; stretchy=&quot;false&quot;>{</mo><mo stretchy=&quot;false&quot;>(</mo><msub><mi>y</mi><mi>j</mi></msub><mo>,</mo><msub><mi mathvariant=&quot;bold-italic&quot;>x</mi><mi>j</mi></msub><mo stretchy=&quot;false&quot;>)</mo><mo>,</mo><mi>j</mi><mo>=</mo><mn>0</mn><mo>&amp;#x2026;</mo><mi>n</mi><mo>&amp;#x2212;</mo><mn>1</mn><mo fence=&quot;false&quot; stretchy=&quot;false&quot;>}</mo></math>">X</span></strong>L={(<em>y</em>j,<strong><em>x</em></strong><em>j</em>),<em>j</em>=0…<em>n</em>−1}XL={(yj,xj),j=0…n−1}.

Let us assume that the true data is generated from a noisy model

<strong><em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot; display=&quot;block&quot;><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo>=</mo><mi>f</mi><mo stretchy=&quot;false&quot;>(</mo><mi mathvariant=&quot;bold-italic&quot;>x</mi><mo stretchy=&quot;false&quot;>)</mo><mo>+</mo><mi mathvariant=&quot;bold-italic&quot;>&amp;#x03F5;</mi><mo>.</mo></math>">y</span></em></strong>=<em>f</em>(<strong><em>x</em></strong>)+<strong><em>ϵ</em></strong>.y=f(x)+ϵ.

Here <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>&amp;#x03F5;</mi></math>">ϵ</span></em>ϵ is normally distributed with mean zero and standard deviation <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msup><mi>&amp;#x03C3;</mi><mn>2</mn></msup></math>">σ</span></em>2σ2.

In our derivation of the ordinary least squares method we defined then an approximation to the function <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>f</mi></math>">f</span></em>f in terms of the parameters <strong><em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi mathvariant=&quot;bold-italic&quot;>&amp;#x03B2;</mi></math>">β</span></em></strong>β and the design matrix <strong><em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi mathvariant=&quot;bold-italic&quot;>X</mi></math>">X</span></em></strong>X which embody our model, that is <strong><em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo mathvariant=&quot;bold&quot; stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mo>=</mo><mi mathvariant=&quot;bold-italic&quot;>X</mi><mi mathvariant=&quot;bold-italic&quot;>&amp;#x03B2;</mi></math>">y</span></em></strong><strong>~</strong>=<strong><em>Xβ</em></strong>y~=Xβ.

The parameters <strong><em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi mathvariant=&quot;bold-italic&quot;>&amp;#x03B2;</mi></math>">β</span></em></strong>β are in turn found by optimizing the means squared error via the so-called cost function

<em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot; display=&quot;block&quot;><mi>C</mi><mo stretchy=&quot;false&quot;>(</mo><mi mathvariant=&quot;bold-italic&quot;>X</mi><mo>,</mo><mi mathvariant=&quot;bold-italic&quot;>&amp;#x03B2;</mi><mo stretchy=&quot;false&quot;>)</mo><mo>=</mo><mfrac><mn>1</mn><mi>n</mi></mfrac><munderover><mo>&amp;#x2211;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>i</mi><mo>=</mo><mn>0</mn></mrow><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>n</mi><mo>&amp;#x2212;</mo><mn>1</mn></mrow></munderover><mo stretchy=&quot;false&quot;>(</mo><msub><mi>y</mi><mi>i</mi></msub><mo>&amp;#x2212;</mo><msub><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mi>i</mi></msub><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup><mo>=</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi mathvariant=&quot;double-struck&quot;>E</mi></mrow><mrow><mo>[</mo><mrow><mo stretchy=&quot;false&quot;>(</mo><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo>&amp;#x2212;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo mathvariant=&quot;bold&quot; stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mo>]</mo></mrow><mo>.</mo></math>">C</span></em>(<strong><em>X</em></strong>,<strong><em>β</em></strong>)=1<em>n</em>∑<em>i</em>=0<em>n</em>−1(<em>y</em>i−<em>y</em>~<em>i</em>)2=E[(<strong><em>y</em></strong>−<strong><em>y</em></strong><strong>~</strong>)2].C(X,β)=1n∑i=0n−1(yi−y~i)2=E[(y−y~)2].

Here the expected value <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi mathvariant=&quot;double-struck&quot;>E</mi></mrow></math>">E</span>E is the sample value.

Show that you can rewrite this as

<span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot; display=&quot;block&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi mathvariant=&quot;double-struck&quot;>E</mi></mrow><mrow><mo>[</mo><mrow><mo stretchy=&quot;false&quot;>(</mo><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo>&amp;#x2212;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo mathvariant=&quot;bold&quot; stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup></mrow><mo>]</mo></mrow><mo>=</mo><mfrac><mn>1</mn><mi>n</mi></mfrac><munder><mo>&amp;#x2211;</mo><mi>i</mi></munder><mo stretchy=&quot;false&quot;>(</mo><msub><mi>f</mi><mi>i</mi></msub><mo>&amp;#x2212;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi mathvariant=&quot;double-struck&quot;>E</mi></mrow><mrow><mo>[</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo mathvariant=&quot;bold&quot; stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mo>]</mo></mrow><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup><mo>+</mo><mfrac><mn>1</mn><mi>n</mi></mfrac><munder><mo>&amp;#x2211;</mo><mi>i</mi></munder><mo stretchy=&quot;false&quot;>(</mo><msub><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi>y</mi><mo stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mi>i</mi></msub><mo>&amp;#x2212;</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi mathvariant=&quot;double-struck&quot;>E</mi></mrow><mrow><mo>[</mo><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mover><mi mathvariant=&quot;bold-italic&quot;>y</mi><mo mathvariant=&quot;bold&quot; stretchy=&quot;false&quot;>&amp;#x007E;</mo></mover></mrow><mo>]</mo></mrow><msup><mo stretchy=&quot;false&quot;>)</mo><mn>2</mn></msup><mo>+</mo><msup><mi>&amp;#x03C3;</mi><mn>2</mn></msup><mo>.</mo></math>">E[(<strong><em>y</em></strong>−<strong><em>y</em></strong><strong>~</strong></span>)2]=1<em>n</em>∑<em>i</em>(<em>f</em>i−E[<strong><em>y</em></strong><strong>~</strong>])2+1<em>n</em>∑<em>i</em>(<em>y</em>~<em>i</em>−E[<strong><em>y</em></strong><strong>~</strong>])2+<em>σ</em>2.E[(y−y~)2]=1n∑i(fi−E[y~])2+1n∑i(y~i−E[y~])2+σ2.

Explain what the terms mean, which one is the bias and which one is the variance and discuss their interpretations.

Perform then a bias-variance analysis of the Franke function by studying the MSE value as function of the complexity of your model.

Discuss the bias and variance trade-off as function of your model complexity (the degree of the polynomial) and the number of data points, and possibly also your training and test data using the <strong>bootstrap</strong> resampling method.

Note also that when you calculate the bias, in all applications you don’t know the function values <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msub><mi>f</mi><mi>i</mi></msub></math>">f</span></em>ifi. You would hence replace them with the actual data points <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><msub><mi>y</mi><mi>i</mi></msub></math>">y</span></em>iyi.

<h3>Part c) Cross-validation as resampling techniques, adding more complexity</h3>

The aim here is to write your own code for another widely popular resampling technique, the so-called cross-validation method. Again, before you start with cross-validation approach, you should scale your data.

Implement the <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>k</mi></math>">k</span></em>k-fold cross-validation algorithm (write your own code) and evaluate again the MSE function resulting from the test folds. You can compare your own code with that from <strong>Scikit-Learn</strong> if needed.

Compare the MSE you get from your cross-validation code with the one you got from your <strong>bootstrap</strong> code. Comment your results. Try <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mn>5</mn><mo>&amp;#x2212;</mo><mn>10</mn></math>">5−10</span>5−10 folds. You can also compare your own cross-validation code with the one provided by <strong>Scikit-Learn</strong>.

<h3>Part d): Ridge Regression on the Franke function with resampling</h3>

Write your own code for the Ridge method, either using matrix inversion or the singular value decomposition as done in the previous exercise or howework 2 (see also chapter 3.4 of Hastie <em>et al.</em>, equations (3.43) and (3.44)). Perform the same bootstrap analysis as in the part b) (for the same polynomials) and the cross-validation part in part c) but now for different values of <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>&amp;#x03BB;</mi></math>">λ</span></em>λ. Compare and analyze your results with those obtained in parts a-c). Study the dependence on <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>&amp;#x03BB;</mi></math>">λ</span></em>λ.

Study also the bias-variance trade-off as function of various values of the parameter <em><span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mi>&amp;#x03BB;</mi></math>">λ</span></em>λ. For the bias-variance trade-off, use the <strong>bootstrap</strong> resampling method. Comment your results.

<h3>Part e): Lasso Regression on the Franke function with resampling</h3>

This part is essentially a repeat of the previous two ones, but now with Lasso regression. Write either your own code (difficult and optional) or, in this case, you can also use the functionalities of <strong>Scikit-Learn</strong> (recommended). Give a critical discussion of the three methods and a judgement of which model fits the data best. Perform here as well an analysis of the bias-variance trade-off using the <strong>bootstrap</strong> resampling technique and an analysis of the mean squared error using cross-validation.

<h3>Part f): Introducing real data and preparing the data analysis</h3>

With our codes functioning and having been tested properly on a simpler function we are now ready to look at real data. We will essentially repeat in part g) what was done in parts a-e). However, we need first to download the data and prepare properly the inputs to our codes. We are going to download digital terrain data from the website <a href="https://earthexplorer.usgs.gov/">https://earthexplorer.usgs.gov/</a>,

In order to obtain data for a specific region, you need to register as a user (free) at this website and then decide upon which area you want to fetch the digital terrain data from. In order to be able to read the data properly, you need to specify that the format should be <strong>SRTM Arc-Second Global</strong> and download the data as a <strong>GeoTIF</strong> file. The files are then stored in <em>tif</em> format which can be imported into a Python program using

scipy.misc.imread

Here is a simple part of a Python code which reads and plots the data from such files

<strong>import</strong> <strong>numpy</strong> <strong>as</strong> <strong>np</strong><strong>from</strong> <strong>imageio</strong> <strong>import</strong> imread<strong>import</strong> <strong>matplotlib.pyplot</strong> <strong>as</strong> <strong>plt</strong><strong>from</strong> <strong>mpl_toolkits.mplot3d</strong> <strong>import</strong> Axes3D<strong>from</strong> <strong>matplotlib</strong> <strong>import</strong> cm <em># Load the terrain</em>terrain1 = imread(‘SRTM_data_Norway_1.tif’)<em># Show the terrain</em>plt.figure()plt.title(‘Terrain over Norway 1′)plt.imshow(terrain1, cmap=’gray’)plt.xlabel(‘X’)plt.ylabel(‘Y’)plt.show()

If you should have problems in downloading the digital terrain data, we provide two examples under the data folder of project 1. One is from a region close to Stavanger in Norway and the other Møsvatn Austfjell, again in Norway. Feel free to produce your own terrain data.

Alternatively, if you would like to use another data set, feel free to do so. This could be data close to your reseach area or simply a data set you found interesting. See for example <a href="https://www.kaggle.com/datasets">kaggle.com</a> for examples.

<h3>Part g) OLS, Ridge and Lasso regression with resampling</h3>

Our final part deals with the parameterization of your digital terrain data (or your own data). We will apply all three methods for linear regression, the same type (or higher order) of polynomial approximation and cross-validation as resampling technique to evaluate which model fits the data best.

At the end, you should present a critical evaluation of your results and discuss the applicability of these regression methods to the type of data presented here (either the terrain data we propose or other data sets).

<h2>Background literature</h2>

<ol>

 <li>For a discussion and derivation of the variances and mean squared errors using linear regression, see the <a href="https://arxiv.org/abs/1509.09169">Lecture notes on ridge regression by Wessel N. van Wieringen</a></li>

 <li>The textbook of <a href="https://www.springer.com/gp/book/9780387848570">Trevor Hastie, Robert Tibshirani, Jerome H. Friedman, The Elements of Statistical Learning, Springer</a>, chapters 3 and 7 are the most relevant ones for the analysis here.</li>

</ol>

<h2>Introduction to numerical projects</h2>

Here follows a brief recipe and recommendation on how to write a report for each project.

<ul>

 <li>Give a short description of the nature of the problem and the eventual numerical methods you have used.</li>

 <li>Describe the algorithm you have used and/or developed. Here you may find it convenient to use pseudocoding. In many cases you can describe the algorithm in the program itself.</li>

 <li>Include the source code of your program. Comment your program properly.</li>

 <li>If possible, try to find analytic solutions, or known limits in order to test your program when developing the code.</li>

 <li>Include your results either in figure form or in a table. Remember to label your results. All tables and figures should have relevant captions and labels on the axes.</li>

 <li>Try to evaluate the reliabilty and numerical stability/precision of your results. If possible, include a qualitative and/or quantitative discussion of the numerical stability, eventual loss of precision etc.</li>

 <li>Try to give an interpretation of you results in your answers to the problems.</li>

 <li>Critique: if possible include your comments and reflections about the exercise, whether you felt you learnt something, ideas for improvements and other thoughts you’ve made when solving the exercise. We wish to keep this course at the interactive level and your comments can help us improve it.</li>

 <li>Try to establish a practice where you log your work at the computerlab. You may find such a logbook very handy at later stages in your work, especially when you don’t properly remember what a previous test version of your program did. Here you could also record the time spent on solving the exercise, various algorithms you may have tested or other topics which you feel worthy of mentioning.</li>

</ul>

<h2>Format for electronic delivery of report and programs</h2>

The preferred format for the report is a PDF file. You can also use DOC or postscript formats or as an ipython notebook file. As programming language we prefer that you choose between C/C++, Fortran2008 or Python. The following prescription should be followed when preparing the report:

<ul>

 <li>Use Canvas to hand in your projects, log in at <a href="https://www.uio.no/english/services/it/education/canvas/">https://www.uio.no/english/services/it/education/canvas/</a> with your normal UiO username and password.</li>

 <li>Upload <strong>only</strong> the report file or the link to your GitHub/GitLab or similar typo of repos! For the source code file(s) you have developed please provide us with your link to your GitHub/GitLab or similar domain. The report file should include all of your discussions and a list of the codes you have developed. Do not include library files which are available at the course homepage, unless you have made specific changes to them.</li>

 <li>In your GitHub/GitLab or similar repository, please include a folder which contains selected results. These can be in the form of output from your code for a selected set of runs and input parameters.</li>

</ul>

Finally, we encourage you to collaborate. Optimal working groups consist of 2-3 students. You can then hand in a common report.

<h2>Software and needed installations</h2>

If you have Python installed (we recommend Python3) and you feel pretty familiar with installing different packages, we recommend that you install the following Python packages via <strong>pip</strong> as

<ol>

 <li>pip install numpy scipy matplotlib ipython scikit-learn tensorflow sympy pandas pillow</li>

</ol>

For Python3, replace <strong>pip</strong> with <strong>pip3</strong>.

See below for a discussion of <strong>tensorflow</strong> and <strong>scikit-learn</strong>.

For OSX users we recommend also, after having installed Xcode, to install <strong>brew</strong>. Brew allows for a seamless installation of additional software via for example

<ol>

 <li>brew install python3</li>

</ol>

For Linux users, with its variety of distributions like for example the widely popular Ubuntu distribution you can use <strong>pip</strong> as well and simply install Python as

<ol>

 <li>sudo apt-get install python3 (or python for python2.7)</li>

</ol>

etc etc.

If you don’t want to install various Python packages with their dependencies separately, we recommend two widely used distrubutions which set up all relevant dependencies for Python, namely

<ol>

 <li><a href="https://docs.anaconda.com/">Anaconda</a> Anaconda is an open source distribution of the Python and R programming languages for large-scale data processing, predictive analytics, and scientific computing, that aims to simplify package management and deployment. Package versions are managed by the package management system <strong>conda</strong></li>

 <li><a href="https://www.enthought.com/product/canopy/">Enthought canopy</a> is a Python distribution for scientific and analytic computing distribution and analysis environment, available for free and under a commercial license.</li>

</ol>

Popular software packages written in Python for ML are

<ul>

 <li><a href="http://scikit-learn.org/stable/">Scikit-learn</a>,</li>

 <li><a href="https://www.tensorflow.org/">Tensorflow</a>,</li>

 <li><a href="http://pytorch.org/">PyTorch</a> and</li>

 <li><a href="https://keras.io/">Keras</a>.</li>

</ul>

These are all freely available at their respective GitHub sites. They encompass communities of developers in the thousands or more. And the number of code developers and contributors keeps increasing.

© 1999-2020, “Data Analysis and Machine Learning FYS-STK3155/FYS4155″:”http://www.uio.no/studier/emner/matnat/fys/FYS3155/index-eng.html”. Released under CC Attribution-NonCommercial 4.0 license