import React,{useEffect, useState} from 'react'
import './Cart.css'
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'
  import { faPlus } from '@fortawesome/free-solid-svg-icons'
  import { faMinus } from '@fortawesome/free-solid-svg-icons'
  import { faTrash } from '@fortawesome/free-solid-svg-icons'
  import { faXmark } from '@fortawesome/free-solid-svg-icons'

const Cart = ({cartpagedata,setCartPageData,closeCart}) => {

  let[ordervalue, setOrderValue] = useState(0);
  let[count, setCount] = useState(0);
  const addmore = <FontAwesomeIcon icon={faPlus} />
  const redqty = <FontAwesomeIcon icon={faMinus} />
  const delcartitem = <FontAwesomeIcon icon={faTrash} />
  const multiply = <FontAwesomeIcon icon={faXmark} />
    
  useEffect(() => {
    const savedCartt = localStorage.getItem('cart');
    if (savedCartt) {
      setCartPageData(JSON.parse(savedCartt));
    }
  }, []);

  console.log(cartpagedata);

  useEffect(() => {
    // Calculate the total order value whenever cartpagedata changes
    let total = 0;
    cartpagedata.forEach((elem) => {
      total += elem.price*elem.Qty;
      
    });
    setOrderValue(total);
    
  }, [cartpagedata]);
  

  return (
    <div className='cartpopup text-white'>
      <ul className='list-unstyled px-4'>

        {
          cartpagedata.map((elem)=>{
           
            return <li key={elem.id} className='d-flex align-items-center justify-content-between border-bottom py-4'>
            <div className='leftcartdiv '>
             <h3 className='item-name'><span className='fs-1'>{elem.id}. </span>{elem.name}</h3>
             <p className='itemprice d-flex align-items-center'>Rs {elem.price} /- <span className='mx-3 fs-3 multiply'>{multiply} </span><span className='fs-3'>{elem.Qty} </span><span className='ms-2'> qty</span> </p>
             
              
            </div>
            <div className='rightcartdiv d-flex align-items-center '>
             <button className='cartbtn fs-6 py-1 px-2'>{redqty}</button>
             <button className='mx-2 cartbtn fs-6 py-1 px-2'>{addmore}</button>
             <button className='cartbtn fs-6 px-2 py-1'>{delcartitem}</button>
              
            </div>
  
          </li>
          total = total + elem.price;
          setOrderValue(total);
          })

        }
        <li className='d-flex align-items-center justify-content-between py-4 totalvaluecart'>
          <div className='totalleft '>
           <h2 className='totalamount'>Total Amount : </h2>
           
           
            
          </div>
          <div className='totalright'>
            <h2 className='text-end'>Rs {ordervalue} /-</h2>
            <div className="pt-5">
              <button className='cartbtn py-2 px-3 fs-5'onClick={closeCart}>Close</button>
              <button className='ms-5 cartbtn py-2 px-3 fs-5'>Order</button>
            </div>
           
            
          </div>

        </li> 

       
        {/* <li className='d-flex align-items-center justify-content-between border-bottom py-4'>
          <div className='leftcartdiv '>
           <h3 className='item-name'>samosa</h3>
           <p className='itemprice d-flex align-items-center'>Rs 15 /- <span className='mx-3 fs-3 multiply'>{multiply} </span><span className='fs-3'>3 Qty</span> </p>
           
            
          </div>
          <div className='rightcartdiv d-flex align-items-center '>
           <button className='cartbtn fs-6 py-1 px-2'>{redqty}</button>
           <button className='mx-2 cartbtn fs-6 py-1 px-2'>{addmore}</button>
           <button className='cartbtn fs-6 px-2 py-1'>{delcartitem}</button>
            
          </div>

        </li>

        <li className='d-flex align-items-center justify-content-between py-4 totalvaluecart'>
          <div className='totalleft '>
           <h2 className='totalamount'>Total Amount : </h2>
           
           
            
          </div>
          <div className='totalright'>
            <h2 className='text-end'>Rs 155 /-</h2>
            <div className="pt-5">
              <button className='cartbtn py-2 px-3 fs-5'>Close</button>
              <button className='ms-5 cartbtn py-2 px-3 fs-5'>Order</button>
            </div>
           
            
          </div>

        </li> */}

      </ul>
      
       
    </div>
  )
}

export default Cart
