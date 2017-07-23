# Notes about RNN/LSTM

[Great Tutorial on this topic](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)

## RNN

- For each time step t, h\_t is computed from h\_(t-1) and x\_t. And h\_t is further passed to the next time step (That's why we always call it hidden states), but this is also regarded as the output of  RNN at the current time step. Usually the output (actually hidden states) will be processed by more operations to get final outputs.

## LSTM 

- In LSTM, the definition of h\_t keeps the same as vanilla RNN - it's the output of the LSTM cell at current time step, and will also be passed to the next step as an input for computing the states(C, the cell states and gates) of next step. So it's still proper to call it a hidden states. 

- The major difference of LSTM is the concept of gates and cell states. Cell state provides a direct link going through the whole time steps without doing any matrix multiplication. **So it's possible to pass the information of far away time steps back to very beginning steps with gate weights being properly learned**, which mitigate the vanishing gradient issue.

- Cell states C and hidden states H are both passed to the next time step, so there are actually two links from the current one to the next, but the hidden state is also considered as LSTM output. Therefore IMO it's more suitable to use **lstm_output** to name the hidden states and use **cell_state** for referring to the C.

- In tensorflow, the lstm cell always return output and state. The output value is a always of size [batch\_size, output\_size (or unit\_size)] **it's the hidden state as discussed above, the returned state is the cell state instead of hidden state.**



