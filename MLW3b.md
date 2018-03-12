

The following piece of code enables us to sort through the eigenvectors and eigenvalues in an ascending order. 
By setting our function as "[srtvecs,srtvals] = eigsort(vecs,vals)," we are sorting our vecs and vals vectors to be acted on by the eigensort command, which will set our values in ascending order. This will make it much easier to visualize the eigenvectors at different energy levels when placed with our PIB code. 

```Matlab
function [ srtvecs,srtvals ] = eigsort( vecs,vals )
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end
```
[Home](/README.md)
