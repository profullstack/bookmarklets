javascript:(async () => {
    const weblnModule = await import('https://unpkg.com/webln@0.3.2/dist/webln.min.js');
    const { webln } = window;

	const findAllNostrPublicKeys = () => {
	    const allElements = document.querySelectorAll('body *');
	    const npubRegex = /npub1[a-zA-Z0-9]+?\b/;
	    const npubIds = [];

	    allElements.forEach(element => {
	        const matches = element.textContent.match(npubRegex);
	        if (matches) {
	            npubIds.push(...matches);
	        }
	    });

	    return npubIds;
	};


    const npubs = findAllNostrPublicKeys();
    console.log(npubs);
    await webln.enable();

    for (let npub of npubs) {
        try {
            const paymentRequest = await webln.makeInvoice();
            await webln.sendPayment(paymentRequest);
        } catch (error) {
            console.error('Error processing payment:', error);
        }
    }
})();





javascript:(async() => {
	const title = document.title;
	const url = window.location.href;

	window.location.href = 'https://othr.us?title='+title+'&url='+url;
})();