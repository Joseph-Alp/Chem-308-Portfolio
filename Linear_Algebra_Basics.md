{% include mathjax.html %}


### Quantum Mechanics Rooted In Linear Algebra

In order to fully utilize the capabilities of MatLab, we must refresh our understanding of linear algebra within the framework of quantum
mechanics. 

# Rows and Columns 

The mechanics behind linear algebra rests within matricies, which are constituted from rows and columns. 
1. *Rows* are mathematically expressed as vectors of 1 x m dimension with a row of m elements:
$$\begin{pmatrix} x_1 & x_2 & x_3 ... & x_n \end{pmatrix}$$
1. *Columns are expressed as vectors with m x 1 dimension and contain a column with m elements: 
$$\begin{pmatrix} x_1\\x_2\\ \vdots \\x_n \end{pmatrix}$$

It is through rows and scalars that we will be developing the concepts of basis sets, and converting between them. 

# Adding Vectors 

Vectors may also be added, taking each element of the vector and adding it to the element in the same position demonstrated as such:
$$\begin{pmatrix} x_1\\x_2\\\vdots\\ x_n \end{pmatrix}+\begin{pmatrix} y_1\\y_2\\\vdots \\y_n \end{pmatrix}=\begin{pmatrix} x_1+y_1\\x_2+y_2\\\vdots\\ x_n+y_n \end{pmatrix}$$

It is paramount that when adding vectors, both the rows and columns must be of the same dimensions; the same is true with matrix addition.

# Multiplying Scalars

Scalar multiplication involves the multiplication of a vector (either row or column) by a scalar, or real number. 
As demonstrated where c represents the scalar quantity: $$c\begin{pmatrix} x_1\\x_2\\ \vdots \\x_n \end{pmatrix}=\begin{pmatrix} c x_1\\c x_2\\\vdots\\ c x_n \end{pmatrix}$$

Additionally, *matrix scalar multiplication* is similar to *vector scalar multiplication* in the sense that each element in 
the matrix is multiplied by the scalar quantity. This is immensely useful for different operators, such as 
momentum and the Hamiltonian, because the operator involves multiplying by a constant, real number. 
In the case of momentum the constant is -i\hbar and for the Hamiltonian the constant is \frac{-\hbar^2}{2m}. We will
touch more upon these principles throughout this course. 

# Inner Product   

Throughout this course, we will utilize the inner product to calculate observables from wave functions. The inner product is 
the product of corresponding elements and their addition, yielding a scalar quantitity. 

If we allow $$\vec q = \begin{pmatrix} x\\y  \end{pmatrix}$$ and $$\vec z=\begin{pmatrix} q\\z
\end{pmatrix}$$, then the inner product of $$\vec q$$ and $$\vec z$$ is $$\langle \vec q, \vec z \rangle =xq+yz.$$

# Normalization 

Normalization is a frequently occuring principle throughout quantum mechanics that allows us 100% certainty in finding our particle's 
wave function adds to 1. 

To get the normalized vector, multiply the vector by a scalar $\displaystyle \frac
1{||\vec q ||}$. This gives the unit vector,  $$\vec w= \frac 1{||\vec q ||} \vec q.$$


