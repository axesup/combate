## Autocomplete Priority

When a user is typing, sometimes it is useful to arrange the autocomplete results so the ones they are most likely to use are displayed first.  For example, here we would like findNearestEnemey to display before findNearestItem, as it is the more common use case.

![](https://lh6.googleusercontent.com/mTf1t4rkqSXfblC2DsJp7bKSZZ-H6dCHCRjlUFdS9EZ7cqGDPN07LfbzEMY83moeNY52GOk27s9IPg6eaJIlxi3PC56JWlM1NtFxGdt9Ejb0cpEza4hd4_rSqHaHd3yjlYW4B-Ik)

To change it’s position, we can add an Autocomplete Priority in the Components editor.  Find the component that provides the function you wish to change and tab to its settings.  Using the add attributes button you can add the property.  

![](https://lh3.googleusercontent.com/BjYFwiuWTOTadDbZigMUe20Qx4C4-duNkW9FzjbEqBWcmsMr7hmFnsnxfQtLFAW8rQHNMtQAvao33hiV1lMdtXOj5uI8uEEbgzVFH8U7mdEWr-2rN2vMa5LJ4Npg4XzRIFzQgHzi)

The default autocomplete priority is 1.  This value acts as  a multiplier, normally a value of 1.2 is enough to boost a method enough relative to closely matching peers. 

## Automatic Variable Capture

Automatic variable capture can be enabled for functions.  When this function is autocompleted as the first expression on a line, an assignment to the named variable is inserted in front of it.

![](https://lh3.googleusercontent.com/pHLORA8hPlkKxh4ui9tyZc6fx0YnIHsA3a74_AaKt9UVzI8VibTX5MlKo1dBwsROBf3feM_o0xudYuqzqD5fEVY0tV_n9lJKdcn7WQSdI2FyihN_iTelh_sXChQ6BdDaGY3lX6Vj)

This feature is best enabled for functions with no side effects, where calling it without using its value makes no sense.