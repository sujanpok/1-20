# 1-20


form.html

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Submission of form</title>
</head>
<body>
    <form method="post" action="/submit">
       <table>
           <tr>
               <td>User name:</td>
               <td><input type="text" id="name" name="name" value="" /></td>
           </tr>
           <tr>
               <td>Gender:</td>
               <td><select id="sex" name="sex">
                       <option value="0">female</option>
                       <option value="1" selected="selected">male</option>
                    </select>
               </td>
           </tr>
           <tr>
               <td>Favorite colors:</td>
               <td>
                   <span>
                       <input type="checkbox"  value="red" id="myColors1" name="myColors" /><input type="hidden" name="_myColors" value="on"/>
                       <label for="myColors1">red</label>
                   </span><span>
                       <input type="checkbox"  value="white" id="myColors2" name="myColors" checked="checked" /><input type="hidden" name="_myColors" value="on"/>
                       <label for="myColors2">white</label>
                   </span><span>
                       <input type="checkbox"  value="black" id="myColors3" name="myColors" checked="checked" /><input type="hidden" name="_myColors" value="on"/>
                       <label for="myColors3">black</label>
                   </span><span>
                       <input type="checkbox"  value="black" id="myColors3" name="myColors" checked="checked" /><input type="hidden" name="_myColors" value="on"/>
                       <label for="myColors3">black</label>
                   </span><span>
                       <input type="checkbox"  value="black" id="myColors3" name="myColors" checked="checked" /><input type="hidden" name="_myColors" value="on"/>
                       <label for="myColors3">black</label>
                   </span>
               </td>
           </tr>
           <tr>
               <td colspan="2">
                   <input type="submit" value="Submission" />
               </td>
           </tr>

       </table>



    </form>
</body>
</html>

 user.java
 
 package com.example.demo;

public class User {
    String name;
    Integer sex;
    String[] MyColors;

    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public Integer getSex() {
        return sex;
    }
    public void setSex(Integer sex) {
        this.sex = sex;
    }
    public String[] getMyColors() {
        return MyColors;
    }
    public void setMyColors(String[] myColors) {
        MyColors = myColors;
    }
}
 



FormController.java


package com.example.demo;

import java.util.Arrays;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class FormController {
    @RequestMapping("/form")
    public String form(Model model){
       
        User user = new User();
        user.setName("");
        user.setSex(1);
        user.setMyColors(new String[]{"white", "black", "black", "black", "black"});
        model.addAttribute("user", user);
        return "form";
    }

    @PostMapping("/submit")
    public String submit(@ModelAttribute User user, Model model){
       
        model.addAttribute("user", user);
        System.out.println("Full name:" + user.getName());
        System.out.println("Gender:" + (user.getSex().intValue() == 1 ? "male" : "female"));
        System.out.println("Favorite colors:" + Arrays.toString(user.getMyColors()));
        //return "redirect:/form";
        return "form";
    }

    
}



