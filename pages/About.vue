<template>
  <div class="container animate__animated animate__fadeIn">
    <div class="row">
      <div class="col-md-6">
        <div class="about">
          <h1 class="line-after">About Me</h1>
          <h4 class="mt-4">Hey 👋</h4>
          <p>
            My name is <b>Murad Mursela</b>, I am an <b>architect</b> and
            <b>graphic designer</b>, passionate about creating logos, brochures,
            and visual identities for brands and projects.
          </p>
          <p>
            I graduated from <u>Wachemo University</u> in Ethiopia and have
            successfully completed many creative design projects. I am
            passionate about design, branding, and delivering unique
            visual experiences for clients and organizations.
          </p>
          <h4 class="mt-5">Creative Skills</h4>
          <p>Below are some of the tools and skills I use daily:</p>
          <div class="row animate__animated animate__fadeInUp">
            <div class="col">
              <ul style="list-style-type: circle;">
                <li>Adobe Photoshop</li>
                <li>Adobe Illustrator</li>
                <li>Logo Design</li>
              </ul>
            </div>
            <div class="col">
              <ul style="list-style-type: circle;">
                <li>Brochure Design</li>
                <li>Brand Identity</li>
                <li>Architecture Concepts</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <img
          src="@/assets/working.png"
          alt="About Illustration"
          class="abt-img"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      stacks: [
        {
          language: "Adobe Photoshop",
          experience: "5+ Years",
          variant: "secondary",
          breif: "Expert in photo editing, mockups, and advanced designs."
        },
        {
          language: "Adobe Illustrator",
          experience: "5+ Years",
          variant: "primary",
          breif: "Skilled in vector graphics, logo design, and branding."
        },
        {
          language: "Logo Design",
          experience: "5+ Years",
          variant: "warning",
          breif: "Created unique logos and identities for brands and projects."
        },
        {
          language: "Brochure & Print Design",
          experience: "4+ Years",
          variant: "success",
          breif: "Designed brochures, flyers, posters, and professional layouts."
        },
        {
          language: "Architecture Concepts",
          experience: "3+ Years",
          variant: "dark",
          breif: "Developed architectural visuals and creative building concepts."
        }
      ]
    };
  },
  head: {
    title: "About 🎨 - Murad Mursela",
    meta: [
      {
        hid: "description",
        name: "description",
        content: `Hey there 👋 My name is Murad Mursela, I am an architect and graphic designer from Ethiopia, passionate about creating logos, brochures, and brand identities. I graduated from Wachemo University and have worked on many successful creative projects.`
      }
    ]
  }
};
</script>

<style scoped>
.container {
  margin-top: 140px;
  text-align: left;
}
.line-after {
  overflow: hidden;
}
.line-after::after {
  content: "";
  display: inline-block;
  height: 0.5em;
  vertical-align: bottom;
  width: 100%;
  margin-right: -100%;
  margin-left: 10px;
  border-top: 2px solid rgb(211, 46, 46);
}
.abt-img {
  width: inherit;
  height: inherit;
  border-radius: 5px;
}
</style>
