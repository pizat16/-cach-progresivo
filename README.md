# -cach-progresivo 
// Service Worker Registration for Production Use - FOR SALE
// Price: $1000 USD
// Description: This script registers a service worker to cache assets locally,
// enabling faster load times and offline functionality for web applications on repeat visits.
// Note: App updates are visible only upon the next visit, as cached resources update in the background.
//
// Key Features:
// - Accelerated load times through asset caching
// - Offline capability for enhanced user experience
// - Update notifications when new content is available

// For more details on this model, read https://goo.gl/KwvDNy

export default function register() {
  if (process.env.NODE_ENV === 'production' && 'serviceWorker' in navigator) {
    window.addEventListener('load', () => {
      const swUrl = `${process.env.PUBLIC_URL}/service-worker.js`;
      navigator.serviceWorker
        .register(swUrl)
        .then(registration => {
          // Listener for service worker updates
          registration.onupdatefound = () => {
            const installingWorker = registration.installing;
            installingWorker.onstatechange = () => {
              if (installingWorker.state === 'installed') {
                if (navigator.serviceWorker.controller) {
                  // Notify of available updates and prompt a refresh
                  console.log('New content is available; please refresh.'); // eslint-disable-line no-console
                } else {
                  // Offline content caching
                  console.log('Content is cached for offline use.'); // eslint-disable-line no-console
                }
              }
            };
          };
        })
        .catch(error => {
          console.error('Error during service worker registration:', error);
        });
    });
  }
}

// Unregister function for the service worker if needed
export function unregister() {
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.ready.then(registration => {
      registration.unregister();
    });
  }
}

// Code available for purchase and deployment at $1000 USD.
// Perfect for developers and businesses seeking optimized performance and offline capabilities in production.
