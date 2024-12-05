<script>
  import facebook from '/assets/images/facebook.png';
  import instagram from '/assets/images/instagram.png';
  import x from '/assets/images/x.png';
  import whatsapp from '/assets/images/whatsapp.png';
</script>

<style>
  @import './Footer.css';
</style>

<div class="footer-father">
  <div class="footer-container">
    <div class="footer-icon-strecher">
      <div class="footer-icon-container">
        <img class="footer-fb-pic" src={facebook} alt="facebook" />
      </div>
      <div class="footer-icon-container">
        <img class="footer-insta-pic" src={instagram} alt="instagram" />
      </div>
      <div class="footer-icon-container">
        <img class="footer-x-pic" src={x} alt="twitter" />
      </div>
      <div class="footer-icon-container">
        <img class="footer-whatsapp-pic" src={whatsapp} alt="whatsapp" />
      </div>
    </div>
    <div class="footer-contact-container">
      <div class="footer-text-container">
        <p class="footer-text-contact">Contacta con nosotros</p>
        <p class="footer-text-email">correo@correo.com</p>
      </div>
    </div>
  </div>
</div>
