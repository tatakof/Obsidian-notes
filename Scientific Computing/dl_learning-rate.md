Deciding how to change our parameters based on the values of the gradients is an important part of the deep learning process. Nearly all approaches start with the basic idea of multiplying the gradient by some small number, called the *learning rate* (LR). The learning rate is often a number between 0.001 and 0.1, although it could be anything. Often, people select a learning rate just by trying a few, and finding which results in the best model after training (we'll show you a better approach later in this book, called the *learning rate finder*). Once you've picked a learning rate, you can adjust your parameters using this simple function:

```

w -= gradient(w) * lr

```

This is known as *stepping* your parameters, using an *optimizer step*.

  

If you pick a learning rate that's too low, it can mean having to do a lot of steps. <<descent_small>> illustrates that.

![[Pasted image 20220720065013.png]]




But picking a learning rate that's too high is even worse—it can actually result in the loss getting *worse*, as we see in!

![[Pasted image 20220720065111.png]]

If the learning rate is too high, it may also "bounce" around, rather than actually diverging; <<descent_bouncy>> shows how this has the result of taking many steps to train successfully.

![[Pasted image 20220720065201.png]]

