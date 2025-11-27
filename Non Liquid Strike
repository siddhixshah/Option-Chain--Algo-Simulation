# option_chain_simulator.py

import streamlit as st

# -----------------------------
# PARAMETERS
# -----------------------------
fair_price = 40
algo_bid = 20
algo_ask = 18
human_buy_threshold_factor = 1.2  # 20% above fair price
human_buy_threshold = fair_price * human_buy_threshold_factor

# -----------------------------
# SIMULATION STATE
# -----------------------------
state = {
    "algo_bid": algo_bid,
    "algo_ask": algo_ask,
    "human_orders": [],
    "transactions": []
}

# -----------------------------
# FUNCTIONS
# -----------------------------

def algo_react(human_price):
    """
    Function to simulate algorithm reaction to human orders
    """
    global state
    transaction = None

    # Step 1: Algo outbids human if human bids above current algo bid
    if human_price > state["algo_bid"]:
        state["algo_bid"] = human_price + 1
        st.write(f"Algo raises bid to {state['algo_bid']}")

    # Step 2: Check if human crosses sell threshold
    if human_price >= human_buy_threshold:
        # Algo sells to human at threshold
        algo_sell_price = human_buy_threshold
        transaction = {"buyer": "human", "seller": "algo", "price": algo_sell_price}
        state["transactions"].append(transaction)
        st.write(f"⚡ Algo sells to human at {algo_sell_price} (20% above fair value)")

        # Reset algo bid/ask after sale
        state["algo_bid"] = 20
        state["algo_ask"] = 100
        st.write(f"🔄 Algo resets bid/ask to {state['algo_bid']}/{state['algo_ask']}")
    
    return transaction

# -----------------------------
# STREAMLIT UI
# -----------------------------
st.title("Option Chain Simulato
