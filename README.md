# Clean-Code

I recall one time I was working on adding a new feature to a project that I have never worked on before, and I read the file that I will add the new feature in, but unfortunately I understood nothing, so I read it one more time, then I asked my colleagues to read it with me, but the guy who wrote that file made sure that no one can understand it ever. So we redeveloped all the file from scratch !!
All that could have been easily avoided if & only if the code was written in a clean way from the first place.


## Functions

Functions are the most important concept in programming, writing it well from the beginning, & making it self-documented "which means that reading the function should be as if you’re reading its documentation" will save you hundreds of hours later when solving an issue or adding a new feature. 

### Small
> the first rule is that functions should be small, & the second rule is that they should be smaller 

It’s advisable to make your functions from 5 lines of code to 20 lines of code maximum,
This will help you in a lot of ways , first it assure that each function does only one task, and it will prevent you from duplicating your code
For example :
```
  const validPhone = (value) => {
    setPhoneValidLoading(true);
    // FIXING ISSUE
    const phoneTemp = /[^0-9]/;
    let temp = [...phoneValidation];
    setShowPhoneValidation(true);
    // console.log('phone', !phoneTemp.test(value));
    if (value.length == 11 && !phoneTemp.test(value)) {
      temp[0].valid = true;
      request(_baseUrls.amanSuper)
        .post(`/amanauth/phone_validation`, { phone_number: value })
        .then((res) => {
          // console.log(res);
          if (res.data.message === "phone_exists") {
            // console.log('phone_exist', res.data.message);
            temp[1].valid = false;
            temp[1].title = strings.all.validate_phone_exist;
            setPhoneValidation(temp);
            setAllPhoneValidation(false);
            setPhoneValidLoading(false);
          } else {
            // console.log('phone_not_exist', res.data.message);
            setPhoneValidLoading(false);

            temp[1].valid = true;
            temp[1].title = strings.all.validate_phone_not_exist;
            setPhoneValidation(temp);
            setShowPhoneValidation(false);
            setAllPhoneValidation(true);
          }
        })
        .catch((err) => {
          /*console.log('checkphone', err.response)*/
        });
    } else {
      temp[0].valid = false;
      temp[1].valid = "notShown";
      setPhoneValidation(temp);
      setAllPhoneValidation(false);
    }
  };

  const changePhoneHandler = (value) => {
    setPhoneNum(value);
    if (value.length > 0) {
      validPhone(value);
    } else {
      setAllPhoneValidation(false);
      setShowPhoneValidation(false);
    }
  };

```
