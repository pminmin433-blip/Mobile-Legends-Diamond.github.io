# Mobile-Legends-Diamond.github.io
const totalDiamonds = selectedProduct ? (selectedProduct.base + selectedProduct.bonus) : 0;
            const price = selectedProduct ? selectedProduct.price.toFixed(2) : '0.00';

            summaryDiamonds.textContent = ${totalDiamonds.toLocaleString()} Diamonds;
            summaryPrice.textContent = USD $${price};
            summaryUserId.textContent = userId && zoneId ? ${userId} (${zoneId}) : 'Awaiting ID Input...';

            // Enable or disable checkout button
            const isReady = selectedProduct && userId && zoneId;
            checkoutButton.disabled = !isReady;
        }

        /**
         * Updates the state variables for User ID and Zone ID inputs.
         * @param {HTMLInputElement} inputElement - The input element that changed.
         */
        function updateInputState(inputElement) {
            if (inputElement.id === 'user-id') {
                userId = inputElement.value.trim();
            } else if (inputElement.id === 'zone-id') {
                zoneId = inputElement.value.trim();
            }
            updateSummary();
        }

        /**
         * Simulated checkout process.
         * In a real Python application, this function would send a request
         * to a Python backend (e.g., Flask/FastAPI endpoint) to handle payment
         * processing and the Mobile Legends API top-up.
         */
        function handleCheckout() {
            if (!selectedProduct) {
                showNotification('Please select a diamond package.', 'error');
                return;
            }

            // Simulate loading state
            const checkoutButton = document.getElementById('checkout-button');
            const originalText = checkoutButton.textContent;
            checkoutButton.textContent = 'Processing...';
            checkoutButton.disabled = true;

            const orderDetails = {
                product: selectedProduct,
                user_id: userId,
                zone_id: zoneId,
                total_price: selectedProduct.price,
                // Conceptually, we'd add payment token/method here
            };

            // --- PYTHON BACKEND SIMULATION (using setTimeout) ---
            console.log('Simulating POST request to Python backend with:', orderDetails);

            setTimeout(() => {
                // Restore button state
                checkoutButton.textContent = originalText;
                checkoutButton.disabled = false;

                // Simple validation check (simulating server response)
                if (userId.length < 5 || zoneId.length === 0) {
                    showNotification('Payment failed: Invalid User/Zone ID format provided.', 'error');
                    console.error('Simulated Server Error: Invalid ID');
                    return;
                }

                // Simulate success
                showNotification(Success! ${selectedProduct.base + selectedProduct.bonus} Diamonds have been credited to User ID ${userId}(${zoneId})., 'success');

                // Reset state for a new order
                selectedProduct = null;
                document.getElementById('user-id').value = '';
                document.getElementById('zone-id').value = '';
                userId = '';
                zoneId = '';
                renderProducts(); // Redraw to clear selection visual
                updateSummary();
            }, 3000); // 3 second delay for realistic simulation
        }

        // --- INITIALIZATION ---
        window.onload = function() {
            renderProducts();
            updateSummary();
            // Attach input listeners (needed if oninput doesn't cover all cases)
            document.getElementById('user-id').addEventListener('input', (e) => updateInputState(e.target));
            document.getElementById('zone-id').addEventListener('input', (e) => updateInputState(e.target));
        };
    </script>
</body>
</html>
