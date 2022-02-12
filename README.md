# information_matrix_under_a_constraint

```
library(MASS)
set.seed(0)



XX<-cbind(rep(1,100),rep(c(1,0),50),rep(c(0,1),50))
XX0<-cbind(rep(c(1,0),50),rep(c(0,1),50))
XX1<-cbind(rep(1,100),rep(c(0,1),50))
yy<-rnorm(100,0.5+rep(c(1,-1),c(50,50)))

beta<-ginv(t(XX)%*%XX)%*%(t(XX)%*%yy)
II<-t(XX)%*%XX
beta0<-MASS::ginv(t(XX0)%*%XX0)%*%(t(XX0)%*%yy)
II0<-t(XX0)%*%XX0
beta1<-MASS::ginv(t(XX1)%*%XX1)%*%(t(XX1)%*%yy)
II1<-t(XX1)%*%XX1

ginv(II)
solve(II0)
solve(II1)

beta[1]-beta[2]-beta[3]==0

CC<-rbind(c(1,1,0),c(1,0,1))

round(CC%*%beta-beta0,4)
round(CC%*%ginv(II)%*%t(CC)-solve(II0),4)
```

## updated

```
library(MASS)
set.seed(0)



XX<-cbind(rep(1,100),rep(c(1,0),50),rep(c(0,1),50))
XX0<-cbind(rep(c(1,0),50),rep(c(0,1),50))
XX1<-cbind(rep(1,100),rep(c(0,1),50))
yy<-rnorm(100,0.5+rep(c(1,-1),c(50,50)))

beta<-ginv(t(XX)%*%XX)%*%(t(XX)%*%yy)
II<-t(XX)%*%XX
beta0<-MASS::ginv(t(XX0)%*%XX0)%*%(t(XX0)%*%yy)
II0<-t(XX0)%*%XX0
beta1<-MASS::ginv(t(XX1)%*%XX1)%*%(t(XX1)%*%yy)
II1<-t(XX1)%*%XX1

ginv(II)
solve(II0)
solve(II1)

beta[1]-beta[2]-beta[3]==0

CC<-rbind(c(1,1,0),c(1,0,1))

round(CC%*%beta-beta0,4)
round(CC%*%ginv(II)%*%t(CC)-solve(II0),4)


##########

# https://en.wikipedia.org/wiki/Ordinary_least_squares#Constrained_estimation
library(Matrix)
XX2<-cbind(rep(1,100),rep(c(0,1),50),rep(c(0,0,0,1),25))

beta2<-c(beta1,0)
II2<-t(XX2)%*%XX2
CC2<-c(0,0,1) # constraint matrix
PP2<-XX2%*%solve(t(XX2)%*%XX2)%*%t(XX2)

beta2_hat<-solve(t(XX2)%*%XX2)%*%(t(XX2)%*%yy)
XXtXXi<-solve(t(XX2)%*%XX2)
beta2<-beta2_hat-XXtXXi%*%CC2%*%solve(t(CC2)%*%XXtXXi%*%CC2)%*%(t(CC2)%*%beta2_hat-0)

XXtXXi-XXtXXi%*%CC2%*%solve(t(CC2)%*%XXtXXi%*%CC2)%*%t(CC2)%*%solve(t(XX2)%*%XX2)%*%CC2%*%solve(t(CC2)%*%XXtXXi%*%CC2)%*%t(CC2)%*%XXtXXi
solve(II1)


ginv(rbind(XX2,CC2))%*%c(t(PP2)%*%yy,0)

solve(II2)
solve(II1)
beta2

```
