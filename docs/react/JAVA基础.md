## React

1. onClick: listen on click then execute the method: this.changeValue()

```js
<button onClick= {() => this.changeValue()}>Subscribe</button>
```



2. callback function

3. ```
       // passing the function as argument
       increCount() {
           this.setState(prev => (
               {
                   count: prev.count + 1
               }
           ));
         console.log()
       }
   ```

4. event - user interaction

5. this keyword undifined:

   solutions:

   ```js
   //solution1
   this.increCount.bind(this)
   // solution2
   () => increCount.bind()
   // solution3
   constructor(){
     this.increCount = this.increCount.bind()
   }
   render(){
     this.increCount
   }
   ```

   

   ```js
           {
            /* <h1>{this.state.value}</h1>
            <Search
              placeholder="input search text"
              onSearch={value => console.log(value)}
              style={{ width: 200 }}
            />
            <br />
            <br />
            <button onClick={() => this.changeValue()}>跳转</button>
            <StarList state={this.state}/> */}
   ```

   ```
               {/* <div className={classes.search}>
                 <div className={classes.searchIcon}></div>
                 <InputBase
                   onChange={handleChange}
                   placeholder="卡片信息"
                   classes={{
                     root: classes.inputRoot,
                     input: classes.inputInput,
                   }}
                   inputProps={{ "aria-label": "search" }}
                 />
                 <SearchIcon />
                 <Button
                   variant="contained"
                   color="primary"
                   onClick={handleSubmit}
                 >
                   Primary
                 </Button>
               </div> */}
   ```

   ```
           {/* {/* <input ref="card_info" onChange={this.inputChange}></input>
           <button onClick={this.handleSubmit}>搜索</button> */}
           <br />
           <br />
           <Stars data={this.state.stars} />
           <br /> */}
   ```

   ```
           <Grid item xs={12} sm={4}>
           <div className={classes.priceRoot}>
             <Typography id="range-slider" variant="body" gutterBottom>
               <br />
               {/* 价格范围 */}
             </Typography>
             <Slider
               value={value}
               onChange={handlePriceChange}
               valueLabelDisplay="on"
               aria-labelledby="range-slider"
               getAriaValueText={valuetext}
               marks={marks}
               max={1000}
               valueLabelFormat={valuetext}
             />
             </div>
           </Grid>
   ```

   

