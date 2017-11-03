# binance-rs
Rust Library for the Binance API

# Usage

Add this to your Cargo.toml

```toml
[dependencies]
binance = "0.1"
```

### GENERAL
```
extern crate binance;

use binance::api::*;
use binance::general::*;

fn main() {
    let general: General = Binance::new(None, None);

    let ping = general.ping();
    match ping {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }   

    let server = general.get_server_time();
    match server {
        Ok(answer) => println!("{}", answer.server_time),
        Err(e) => println!("Error: {}", e),
    }
}
```

### MARKET DATA
```
extern crate binance;

use binance::api::*;
use binance::market::*;

fn main() {
    let market: Market = Binance::new(None, None);
    match market.get_depth("KNCETH".into()) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }         

    match market.get_price("KNCETH".into()) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    } 

    match market.get_book_ticker("KNCETH".into()) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }
}
```

### USER STREAM
```
extern crate binance;

use binance::api::*;
use binance::userstream::*;

fn main() {
    let api_key = Some("YOUR_API_KEY".into());
    let user_stream: UserStream = Binance::new(api_key, None);
    
    match user_stream.start() {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    } 

    match user_stream.keep_alive("listen_key") {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }     

    match user_stream.close("listen_key") {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }      
}
```

### ACCOUNT DATA
```
extern crate binance;

use binance::api::*;
use binance::account::*;

fn main() {
    let api_key = Some("YOUR_API_KEY".into());
    let secret_key = Some("YOUR_SECRET_KEY".into());

    let account: Account = Binance::new(api_key.clone(), secret_key);
   
    match account.get_account() {
        Ok(answer) => println!("{:?}", answer.balances),
        Err(e) => println!("Error: {}", e),
    }
    
    match account.get_open_orders("WTCETH".into()) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    } 

    match account.limit_buy("WTCETH".into(), 10, 0.014000) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }

    match account.market_buy("WTCETH".into(), 5) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }

    match account.limit_sell("WTCETH".into(), 10, 0.035000) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }

    match account.market_sell("WTCETH".into(), 5) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }

    match account.order_status("WTCETH".into(), 1957528) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }

    match account.cancel_order("WTCETH".into(), 1957528) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }   

    match account.get_balance("KNC".into()) {
        Ok(answer) => println!("{:?}", answer),
        Err(e) => println!("Error: {}", e),
    }
}
```