Site Acessivel
· html
// scripts/script.js


const form = document.querySelector('form');
const modal = document.querySelector('#modal');
const fecharModal = document.querySelector('#fechar-modal');
let ultimoFoco;


// Mostra o modal e mantém o foco nele
defineFocusTrap = () => {
  ultimoFoco = document.activeElement;
  modal.classList.remove('hidden');
  modal.querySelector('button').focus();
  document.addEventListener('keydown', trapFocus);
};


// Fecha o modal e devolve o foco ao último elemento
const closeModal = () => {
  modal.classList.add('hidden');
  document.removeEventListener('keydown', trapFocus);
  ultimoFoco.focus();
};


// Mantém o foco dentro do modal
const trapFocus = (e) => {
  const focusableElements = modal.querySelectorAll('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])');
  const first = focusableElements[0];
  const last = focusableElements[focusableElements.length - 1];


  if (e.key === 'Tab') {
    if (e.shiftKey) {
      if (document.activeElement === first) {
        e.preventDefault();
        last.focus();
      }
    } else {
      if (document.activeElement === last) {
        e.preventDefault();
        first.focus();
      }
    }
  }
  if (e.key === 'Escape') {
    closeModal();
  }
};


form.addEventListener('submit', (e) => {
  e.preventDefault();
  defineFocusTrap();
});


fecharModal.addEventListener('click', closeModal);
