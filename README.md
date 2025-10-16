# hiransupplements
hiran supplements are the best supplements in the market
import React, { useState, useEffect } from 'react';
import { motion, useAnimation } from 'framer-motion';
import { useInView } from 'react-intersection-observer';

const products = [
  {
    id: 1,
    name: 'Hiran Creatine Monohydrate',
    description: 'Boost your strength and endurance with pure creatine.',
    price: '₹1,499',
    img: 'https://via.placeholder.com/400x400.png?text=Creatine'
  },
  {
    id: 2,
    name: 'Hiran Protein Blend',
    description: 'Accelerate muscle recovery and growth.',
    price: '₹1,999',
    img: 'https://via.placeholder.com/400x400.png?text=Protein'
  }
];

export default function Hiran() {
  const [email, setEmail] = useState('');
  const [subscribed, setSubscribed] = useState(false);
  const [cart, setCart] = useState([]);
  const [checkoutComplete, setCheckoutComplete] = useState(false);

  const handleSubscribe = (e) => {
    e.preventDefault();
    if(email) setSubscribed(true);
  };

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  const handleCheckout = () => {
    if(cart.length > 0){
      setCheckoutComplete(true);
      setCart([]);
    }
  };

  const [ref, inView] = useInView({ threshold: 0.2 });
  const controls = useAnimation();

  useEffect(() => {
    if (inView) {
      controls.start({ opacity: 1, y: 0, transition: { duration: 0.8 } });
    }
  }, [controls, inView]);

  return (
    <div className="min-h-screen bg-black text-white font-sans antialiased overflow-x-hidden">
      {/* Hero */}
      <section className="flex flex-col md:flex-row items-center justify-between max-w-6xl mx-auto py-16 px-6 relative overflow-hidden">
        <motion.div initial={{ x: -50, opacity: 0 }} animate={{ x:0, opacity:1 }} transition={{ duration: 0.6 }}>
          <h1 className="text-5xl md:text-6xl font-bold text-white drop-shadow-md">Hiran</h1>
          <p className="mt-4 text-gray-300 text-lg max-w-md">Engineered for Strength. Premium supplements to fuel your performance.</p>
          <div className="mt-6 flex gap-4">
            <a href="#products" className="px-6 py-3 bg-white text-black rounded-lg font-semibold hover:bg-gray-200 transition duration-300">Shop Now</a>
            <a href="#about" className="px-6 py-3 border border-white rounded-lg hover:bg-gray-900 transition duration-300">Learn More</a>
          </div>
        </motion.div>
        <motion.div initial={{ scale: 0.9, opacity:0 }} animate={{ scale:1, opacity:1 }} transition={{ duration:0.6 }} className="mt-10 md:mt-0 relative overflow-visible">
          <motion.img src="https://via.placeholder.com/400x400.png?text=Hiran+Jar" alt="Hiran Supplement Jar" className="rounded-xl shadow-2xl drop-shadow-white transform hover:scale-105 transition duration-500" animate={{ y: inView ? [0, -20, 0] : 0 }} transition={{ duration: 4, repeat: Infinity, ease: 'easeInOut' }} />
          <div className="absolute top-0 left-0 w-full h-full pointer-events-none" style={{ background: 'radial-gradient(circle, rgba(255,255,255,0.2) 0%, transparent 70%)' }} />
        </motion.div>
      </section>

      {/* Products */}
      <section id="products" className="py-16 bg-gray-900">
        <div className="max-w-6xl mx-auto px-6">
          <h2 className="text-4xl font-bold mb-10 text-center drop-shadow-md">Our Products</h2>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-10">
            {products.map(p => (
              <motion.div ref={ref} animate={controls} initial={{ opacity: 0, y: 50 }} whileHover={{ scale: 1.05, boxShadow: '0 0 20px #fff' }} className="bg-black rounded-xl p-6 shadow-lg flex flex-col items-center text-center border border-gray-700 hover:border-white transition duration-300">
                <img src={p.img} alt={p.name} className="w-48 h-48 object-cover rounded-xl mb-4 shadow-xl" />
                <h3 className="text-xl font-semibold mb-2 drop-shadow-md">{p.name}</h3>
                <p className="text-gray-400 mb-2">{p.description}</p>
                <p className="text-white font-bold mb-4 text-lg">{p.price}</p>
                <button onClick={()=>addToCart(p)} className="px-4 py-2 bg-white text-black rounded-lg font-semibold hover:bg-gray-200 transition duration-300">Add to Cart</button>
              </motion.div>
            ))}
          </div>
          {cart.length > 0 && (
            <motion.div ref={ref} animate={controls} initial={{ opacity:0, y:20 }} className="mt-10 text-center">
              <h3 className="text-2xl font-bold mb-4">Cart Summary</h3>
              <ul className="mb-4">
                {cart.map((item, index) => <li key={index}>{item.name} - {item.price}</li>)}
              </ul>
              <button onClick={handleCheckout} className="px-6 py-3 bg-white text-black rounded-lg font-semibold hover:bg-gray-200 transition duration-300">Checkout</button>
            </motion.div>
          )}
          {checkoutComplete && <p className="text-green-400 mt-4 text-center">Thank you for your purchase!</p>}
        </div>
      </section>

      {/* About / Why Hiran */}
      <section id="about" className="py-16 max-w-6xl mx-auto px-6 relative">
        <h2 className="text-4xl font-bold mb-6 text-center drop-shadow-md">Why Hiran?</h2>
        <motion.p ref={ref} animate={controls} initial={{ opacity:0, y:20 }} className="text-gray-300 text-center max-w-3xl mx-auto text-lg">Hiran supplements are crafted with premium ingredients, backed by science, and designed for athletes and fitness enthusiasts who demand performance and recovery at the highest level.</motion.p>
        <div className="mt-12 flex justify-center">
          <form onSubmit={handleSubscribe} className="flex flex-col sm:flex-row gap-4">
            <input type="email" placeholder="Enter your email" value={email} onChange={e=>setEmail(e.target.value)} className="p-3 rounded-lg text-black w-64" required />
            <button type="submit" className="px-6 py-3 bg-white text-black rounded-lg font-semibold hover:bg-gray-200 transition duration-300">Join Hiran Club</button>
          </form>
        </div>
        {subscribed && <p className="text-green-400 mt-4 text-center">Thanks for subscribing!</p>}
      </section>

      {/* Footer */}
      <footer className="bg-black py-8 text-center text-gray-400">
        © {new Date().getFullYear()} Hiran. All rights reserved.
      </footer>
    </div>
  );
}
