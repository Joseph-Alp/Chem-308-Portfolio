[home](/README.md)


The following piece of code enables us to sort through the eigenvectors and eigenvalues in an ascending order. 

Content is based on notes taken on 1/25/18, and PIB handout.

function [ srtvecs,srtvals ] = eigsort( vecs,vals )
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end
