<template>
    <form @submit.prevent="handleSubmit">
        <!-- "@submit" is used to handle submit. -->

        <!-- " @submit.prevent" can prevent the form from obeying the default rule of forms(which is, to refresh after submitting). -->
        <h1 style="text-align: center; color:blue; text-shadow: 5px 7px 6px brown; font-size: 55px;">JOB APPLICATION</h1>
        <label for="">Email:</label>

        <input type="email" placeholder="abc@xyz.com" v-model="email" required /> <br><br>

        <label for="">Password:</label>

        <input type="password" placeholder="Enter Password" v-model="password" required />
        <div class="password__error" v-if="passwordError"> {{ passwordError }} </div> <br><br>
        <!-- This is to display the password validation message. -->

        <label for="">Experience Level:</label> <br />

        <select v-model="level" style="padding: 10px" required>
            <option value="Beginner">Beginner</option>

            <option value="Amateur">Amateur</option>

            <option value="Intermediate">Intermediate</option>

            <option value="Professional">Professional</option>

            <option value="Expert">Expert</option>
        </select>
        <br><br>

        <!-- SKILLS       SKILLS      SKILLS -->

        <label for="skills">Programming Skill(s):</label> <br>
        <span style="color:indigo; font-size:25px">Press alt + comma (",") to save skills</span> <br><br>

        <input type="text" placeholder="Enter your skills" v-model="tempSkill" @keyup.alt="addSkill" />

        <!-- I added ".alt" coz my keyup event here is "comma" and I don't want to see it in my output. So by adding alt here, the "comma is still gonna do its work but it's not gonna appear as an output. When you press any key/letter with some special keys like alt, ctrl, shift, etc, the keys/letters you press will be triggered but they won't show as an output  -->

        <!-- This is the field for skill(s) the User type(s) in. The skill(s) will be added to the Skill set array/folder. -->

        <!-- @keyup fires when the user presses a key and lifts finger up. -->

        <div v-for="skill in softSkills" :key="skill" class="pill">
            <span title="Click to remove" @click="deleteSkill(skill)">{{ skill }}</span>

            <!-- "skill" was used to loop, therefore I have access to the individual skills. -->

            <!-- There is an argument(skill) in the function coz I want to delete a particular skill. -->
        </div> <br> <br>
        <span v-if="softSkills != ''" style="color:red; font-size:25px">Click on each skill to delete</span>
        <br><br>
        <!-- This will display only if we have chosen some skills already. It should not display if we have no skill. -->
        <!-- v:for is for looping, and looping needs :key and that should be unique for each skill -->



        <label>Additional skills:</label>

        <div class="terms">
            <input type="checkbox" value="Good team player" v-model="additional_skills" />

            <label for="">Good team player</label>
        </div>

        <div class="terms">
            <input type="checkbox" value="Microsoft Office Proficiency" v-model="additional_skills" />

            <label for="">Microsoft Office Proficiency</label>
        </div>

        <div class="terms">
            <input type="checkbox" value="Research and Analysis" v-model="additional_skills" />

            <label for="">Research and Analysis</label>
        </div> <br><br>



        <div class="terms">
            <input type="checkbox" name="" v-model="terms" id="" style="" required />

            <label for="">Accept Terms & Conditions</label>
        </div>



        <div class="submit">
            <button style="font-size: 30px;" type="submit">Submit</button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            email: "",
            password: "",
            level: "Beginner",
            terms: false,
            additional_skills: [],
            tempSkill: "",
            // This is just a temporary field for each skill user types.
            softSkills: [],
            // This is the set of skills (array)
            passwordError: "",
            //Needed for Password validation
        };
    },
    methods: {
        addSkill(e) {
            // I need that argument 'e' coz we have to listen to a particular keyboard event (keyup).
            // console.log(e);
            // Just to log to the console whatever key you press at the call of the eventListener.
            if (e.key === "," && this.tempSkill) {
                // I made sure 'comma' is the key. This function fires when the user click 'comma' and lifts finger up. And also, there must be something in the field (tempSkill). i.e you can't just click on only 'comma'. There has to be something in the field. The field should not be empty. This is because I want to be saving every text user types. Whenever comma is triggered, it wil save the text before the comma.
                if (!this.softSkills.includes(this.tempSkill)) {
                    // I don't want duplicates. Users shouldn't write the same skill twice. So this function is making sure they haven't already provided the same skill they wanna provide now.
                    this.softSkills.push(this.tempSkill);
                    //Then after fulfilling ALL the above conditions, this is to save / push anything user types in the tempSkill inside the softSkills array.
                }
                this.tempSkill = "";
                // This is to clear up the input box for users to type more. It pushes to softSkills array whatever users type in the tempSkill box and then clears the box immediately.
            }
        },
        deleteSkill(skill) {

            this.softSkills = this.softSkills.filter((item) => {

                // filter() cycles through an array and fires the function for each item in the array. If I return 'true' for an item in the array, then the array is still gonna keep that particular item, but if I return 'false', that item will be removed from the array.

                return skill !== item

                // "item" is used to represent all the stuffs in the array.
                // "skill" is used to represent the current stuff we're clicking on.
                // And by returning false here, it means the array is gonna remove SKILL(current thing we clicked on) from ITEM(all the stuffs in the array).
            })
        },
        handleSubmit() {
            //Password validation
            this.passwordError = this.password.length > 5 ?
                '' : 'Sorry.....Password must be 8 chars long'
            // This is Ternary Operator. Here, if the password's length is greater than 5, it's gonna save null into the passwordError and if not, it's gonna put the error into the passwordError.
            if (!this.passwordError) {
                console.log('Email: ', this.email)
                console.log('Password: ', this.password)
                console.log('Experience level: ', this.level)
                console.log('Skills: ', this.softSkills)
                console.log('Additional Skills: ', this.additional_skills)
                console.log('Terms accepted: ', this.terms)
                alert("Application submitted. We'll get in touch very soon.    :)")
            } else {
                alert(this.passwordError)
                console.log("Sorry, kindly follow the Password rules")
            }
        }
    }
}
</script>

<style>
form {
    max-width: 1200px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 1.3em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input,
select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    font-size: 25px;
}

input:focus,
select:focus {
    outline: none;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 35px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}

button {
    background: green;
    border: 0;
    padding: 10px 20px;
    color: white;
    border-radius: 20px;
    margin-top: 20px;
    cursor: pointer
}

.submit {
    text-align: center;
}

.password__error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 25px;
    font-weight: bold;
}
</style>
