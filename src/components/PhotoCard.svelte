<script>
    let { photoUrl, text, rotate, position } = $props();
    rotate = rotate || 0;

    import { onMount } from 'svelte';
  let width;
  
  onMount(() => {
    // Set initial width
    width = window.innerWidth;
    
    // Update width on resize
    const handleResize = () => {
      width = window.innerWidth;
    };
    
    window.addEventListener('resize', handleResize);
    
    // Cleanup
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  });

</script>


<div class="polaroid" style:rotate="{rotate}deg" style:left="{(width /4) + position}px"> 
    <img width="200" height="200" class="rounded-md" src="{photoUrl}" alt="photos of me"/> 
    <h3 class="text-xl font-bold text-center text-black">{text}</h3>
</div>

<style>
    .polaroid {
        position: absolute;
        width: 200px;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1rem;
        border: 2px solid white;
        border-radius: 0.5rem;
        background-color: white;
        padding: 1rem;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    }

    .polaroid:hover {
        z-index: 9999;
        transform: scale(1.1);
    }
</style>